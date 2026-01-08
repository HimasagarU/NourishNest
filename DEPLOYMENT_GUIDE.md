# Deploying NourishNest to Vercel 🚀

A comprehensive guide to deploy your NourishNest Node.js/Express application to Vercel with MongoDB Atlas.

## Prerequisites

Before you begin, ensure you have:
- A [Vercel](https://vercel.com) account (sign up at vercel.com)
- A [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) account with a running cluster
- Git and Node.js installed locally
- Your NourishNest repository pushed to GitHub

## Step 1: Prepare Your Application

### Update your `index.js` file

Ensure your main entry point is named `index.js` in the root directory:

```javascript
const express = require('express');
const mongoose = require('mongoose');
const dotenv = require('dotenv');
const cors = require('cors');

dotenv.config();

const app = express();

// Middleware
app.use(express.json());
app.use(cors());

// MongoDB Connection
mongoose.connect(process.env.MONGODB_URI, {
  useNewUrlParser: true,
  useUnifiedTopology: true
})
.then(() => console.log('MongoDB connected'))
.catch(err => console.log(err));

// Routes
app.use('/api', require('./routes'));

// Serve static files
app.use(express.static('public'));

// Listen on port
const PORT = process.env.PORT || 5000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});

module.exports = app;
```

## Step 2: Create `vercel.json` Configuration

Create a `vercel.json` file in your root directory:

```json
{
  "version": 2,
  "builds": [
    {
      "src": "index.js",
      "use": "@vercel/node"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "index.js"
    }
  ]
}
```

## Step 3: Create `.env.local` (For Local Testing)

Create a `.env.local` file in your root directory (do NOT commit this):

```
MONGODB_URI=mongodb+srv://your-username:your-password@cluster-name.mongodb.net/database-name?retryWrites=true&w=majority
PORT=5000
NODE_ENV=development
```

## Step 4: Set Up MongoDB Atlas

### Get Your MongoDB Connection String:

1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Log in to your account
3. Select your cluster
4. Click "Connect"
5. Choose "Connect your application"
6. Copy the connection string (replace `<password>` with your database user password)

Example format:
```
mongoodb+srv://username:password@cluster0.xxxxx.mongodb.net/nourishNest?retryWrites=true&w=majority
```

## Step 5: Deploy to Vercel

### Option A: Deploy via GitHub (Recommended)

1. **Push your code to GitHub**
   ```bash
   git add .
   git commit -m "Add deployment configuration"
   git push origin main
   ```

2. **Go to [Vercel Dashboard](https://vercel.com/dashboard)**

3. **Click "Add New" → "Project"**

4. **Select your GitHub repository** (NourishNest)

5. **Configure Project Settings:**
   - Framework Preset: `Other`
   - Root Directory: `./` (default)
   - Build Command: Leave empty (no build needed)
   - Output Directory: Leave empty
   - Install Command: `npm install`

6. **Click "Deploy"**

### Option B: Deploy via Vercel CLI

1. **Install Vercel CLI**
   ```bash
   npm install -g vercel
   ```

2. **Login to Vercel**
   ```bash
   vercel login
   ```

3. **Deploy Your Application**
   ```bash
   vercel
   ```

4. **Follow the prompts:**
   - Set up and deploy? Yes
   - Which scope do you want to deploy to? (Select your account)
   - Link to existing project? No (for first deployment)
   - What's your project's name? nourishnest
   - In which directory is your code? ./
   - Want to modify these settings? No

## Step 6: Add Environment Variables

### Via Vercel Dashboard:

1. **Go to Vercel Dashboard** → **Select your project**

2. **Click "Settings" → "Environment Variables"**

3. **Add the following variables:**

   | Variable Name | Value |
   |---|---|
   | `MONGODB_URI` | `mongodb+srv://username:password@cluster.mongodb.net/nourishNest?retryWrites=true&w=majority` |
   | `NODE_ENV` | `production` |

4. **Click "Save"**

5. **Redeploy your project:**
   - Go to "Deployments"
   - Click the three dots on the latest deployment
   - Select "Redeploy"

### Via Vercel CLI:

```bash
vercel env add MONGODB_URI
# Enter your MongoDB connection string when prompted

vercel env add NODE_ENV
# Enter: production
```

Then redeploy:
```bash
vercel --prod
```

## Step 7: Test Your Deployment

1. **Visit your Vercel deployment URL** (shown in dashboard or CLI output)
   Example: `https://nourishnest.vercel.app`

2. **Test API endpoints:**
   ```bash
   curl https://yourdomain.vercel.app/api/meals
   ```

3. **Check server logs:**
   - Go to Vercel Dashboard → Project → Deployments
   - Click on your deployment
   - View "Functions" or "Logs" tab

## Troubleshooting

### Issue: MongoDB Connection Error

**Error:** `MongoParseError: Invalid scheme, expected connection string to start with "mongodb://" or "mongodb+srv://"`

**Solution:**
- Verify your `MONGODB_URI` environment variable is set correctly
- Make sure it starts with `mongodb+srv://`
- Check that you've added the IP whitelist in MongoDB Atlas (or allow all IPs: 0.0.0.0/0)
- Redeploy after updating environment variables

### Issue: 404 Not Found Errors

**Solution:**
- Ensure your `vercel.json` file is properly configured
- Check that all routes are properly defined in your Express app
- Verify that static files are being served from the `public` directory

### Issue: CORS Errors

**Solution:**
```javascript
const cors = require('cors');

app.use(cors({
  origin: process.env.FRONTEND_URL || '*',
  credentials: true
}));
```

Add `FRONTEND_URL` environment variable in Vercel if needed.

### Issue: Build Timeout

**Solution:**
- Optimize your dependencies
- Remove unused packages
- Consider splitting your app into smaller functions

## Environment Variables Reference

```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/dbname?retryWrites=true&w=majority
NODE_ENV=production
PORT=5000 (optional, Vercel sets this automatically)
JWT_SECRET=your_jwt_secret_key (if using authentication)
API_KEY=your_api_keys (if using external APIs)
```

## Viewing Deployment Logs

### Via Vercel Dashboard:
1. Go to your project
2. Click "Deployments"
3. Select the deployment you want to view
4. Click "Logs"

### Via Vercel CLI:
```bash
vercel logs [url] --tail
```

## Updating Your Deployment

### Method 1: GitHub Integration (Automatic)
Just push changes to GitHub, and Vercel will automatically redeploy.

```bash
git add .
git commit -m "Your commit message"
git push origin main
```

### Method 2: Manual Redeploy
```bash
vercel --prod
```

## Production Best Practices

1. **Use Environment Variables** - Never hardcode secrets
   ```javascript
   const dbUri = process.env.MONGODB_URI;
   ```

2. **Set NODE_ENV to Production**
   ```bash
   NODE_ENV=production
   ```

3. **Enable HTTPS** - Vercel provides free HTTPS automatically

4. **Configure CORS Properly**
   ```javascript
   app.use(cors({
     origin: ['https://yourdomain.com'],
     credentials: true
   }));
   ```

5. **Use MongoDB Connection Pooling**
   ```javascript
   mongoose.connect(process.env.MONGODB_URI, {
     maxPoolSize: 10,
   });
   ```

6. **Enable Rate Limiting**
   ```bash
   npm install express-rate-limit
   ```

## Custom Domain Setup

1. **Go to Vercel Project Settings**
2. **Click "Domains"**
3. **Add your domain**
4. **Follow DNS configuration instructions**
5. **Update your domain's nameservers**

## Monitoring and Analytics

Vercel provides:
- **Analytics**: Go to "Analytics" tab in your project
- **Error Tracking**: Automatic error logs in deployments
- **Performance Metrics**: View build times and response times

## Common Commands

```bash
# Deploy to production
vercel --prod

# View logs
vercel logs [url] --tail

# Set environment variables
vercel env add VARIABLE_NAME

# List all deployments
vercel list

# Remove a deployment
vercel remove [deployment-url]

# Inspect deployment
vercel inspect [deployment-url]
```

## Useful Links

- [Vercel Documentation](https://vercel.com/docs)
- [Vercel Express Guide](https://vercel.com/docs/frameworks/express)
- [MongoDB Atlas Documentation](https://docs.mongodb.com/atlas)
- [Vercel Environment Variables](https://vercel.com/docs/environment-variables)
- [Node.js Deployment Guide](https://nodejs.org/en/docs/guides/nodejs-docker-webapp/)

## Getting Help

- Check Vercel [status page](https://www.vercelstatus.com)
- Review [Vercel community forums](https://community.vercel.com)
- Check [MongoDB documentation](https://docs.mongodb.com)
- File an issue on [GitHub](https://github.com/HimasagarU/NourishNest/issues)

---

**Congratulations! 🎉** Your NourishNest application is now deployed on Vercel and ready to serve users worldwide!

For more information on managing your deployment, visit the [Vercel Dashboard](https://vercel.com/dashboard).
