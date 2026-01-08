# NutriPath Pro

A comprehensive nutrition and diet planning platform designed to help users achieve their health goals through intelligent meal planning, real-time nutrition tracking, and personalized dietary recommendations.

## 🎯 Overview

NutriPath Pro is a full-stack responsive web application that combines modern UI/UX with powerful backend functionality. It provides users with comprehensive nutrition data, recipe suggestions, meal planning tools, and progress tracking features—all wrapped in an intuitive interface designed for accessibility and ease of use.

## ✨ Key Features

- **Interactive & Responsive Design** - Seamless experience across all devices (mobile, tablet, desktop)
- **Advanced Recipe Database** - Browse recipes with detailed nutrition information and cooking instructions
- **Nutrition Index & Analysis** - Real-time macronutrient and micronutrient tracking
- **BMI Calculator** - Health metrics calculation with personalized recommendations
- **Diet Management** - Track calories and plan diets based on health goals
- **Admin Dashboard** - Comprehensive admin panel for content management
- **Secure Authentication** - User authentication and authorization with session management
- **User Feedback System** - Collect and manage user feedback
- **Real-time API Integration** - Meal API integration with Axios for dynamic data fetching
- **Progress Tracking** - Visual progress tracking for diet and nutrition goals

## 🛠️ Technology Stack

**Frontend:**
- HTML5 / CSS3 / JavaScript
- EJS (Embedded JavaScript Templating)
- Responsive Design (Mobile-first approach)

**Backend:**
- Node.js with Express.js
- MongoDB (NoSQL Database)
- Axios (HTTP Client for API Integration)

**Tools & Services:**
- npm (Package Management)
- Vercel (Deployment)
- Third-party Meals API

## 📊 Project Structure

```
NourishNest/
├── src/              # Source code (backend logic)
├── views/            # EJS templates (frontend pages)
├── public/           # Static assets (CSS, images)
├── Screenshots/      # Project screenshots
├── package.json      # Dependencies and scripts
├── index.js          # Entry point
└── README.md         # Documentation
```

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- npm or yarn
- MongoDB account and connection string

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/HimasagarU/NourishNest.git
cd NourishNest
```

2. **Install dependencies**
```bash
npm install
```

3. **Configure environment variables**
```bash
# Create a .env file in the root directory
# Add your MongoDB connection string:
MONGODB_URI=your_mongodb_connection_string
PORT=3000
```

4. **Update database configuration**
Edit `index.js` and add your MongoDB URL to the connection string.

5. **Start the development server**
```bash
npm run dev
```

The application will be available at `http://localhost:3000`

## 📋 Features in Detail

### Nutrition Tracking
- Comprehensive nutritional information for recipes
- Macronutrient breakdown (proteins, carbs, fats)
- Micronutrient analysis (vitamins, minerals)
- Daily intake recommendations

### Meal Planning
- Browse extensive recipe database
- Filter recipes by cuisine, diet type, and nutrition
- Create custom meal plans
- Track daily calories and nutrients

### User Management
- Secure user authentication
- Personalized user profiles
- Save favorite recipes and meal plans
- Track progress over time

### Admin Panel
- Manage recipes and nutritional data
- User management and analytics
- Feedback review and management
- Content administration

## 📸 Screenshots

### Dashboard
Main interface with user statistics and quick access to features.

### Recipe Browser
Search and filter recipes with detailed nutrition information.

### Meal Planner
Create and manage personalized meal plans.

### Nutrition Dashboard
Track daily intake and view detailed nutritional analysis.

### Admin Panel
Manage content and user data.

## 🔧 API Integration

The application uses the **Meals API** for dynamic recipe data:
- Endpoint: `https://www.themealdb.com/api/json/v1/1/search.php?s={meal}`
- Provides detailed recipe information including ingredients and instructions

## 📈 Usage Examples

### For Users
1. Register and create a profile
2. Browse recipes and add to favorites
3. Create a meal plan
4. Track daily nutrition intake
5. Monitor progress and adjust diet

### For Admins
1. Log in to admin panel
2. Add/edit/delete recipes
3. Manage diet categories
4. Review user feedback
5. View platform analytics

## 🎨 Design Highlights

- **Clean UI** - Minimal, intuitive design focused on usability
- **Responsive Layout** - Optimized for all screen sizes
- **Accessibility** - WCAG compliant with keyboard navigation
- **Performance** - Optimized loading times and smooth interactions
- **User-Centric** - Designed based on user feedback and testing

## 📝 License

This project is open source and available under the MIT License.

## 👨‍💻 Author

**Himasagar U**
- GitHub: [@HimasagarU](https://github.com/HimasagarU)

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📞 Support

If you encounter any issues or have questions, please open an issue on the GitHub repository.

---

**Last Updated:** January 2026
**Status:** Active Development
