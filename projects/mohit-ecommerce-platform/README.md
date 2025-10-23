# 🛒 Mohit's E-Commerce Platform

A modern, full-stack e-commerce platform built with React, Node.js, and MongoDB. This project demonstrates real-world application development with features like user authentication, product management, shopping cart, payment integration, and admin dashboard.

## 🚀 Features

### Customer Features
- ✅ User Registration & Authentication
- ✅ Product Browsing & Search
- ✅ Shopping Cart Management
- ✅ Secure Checkout Process
- ✅ Order History & Tracking
- ✅ User Profile Management
- ✅ Product Reviews & Ratings
- ✅ Wishlist Functionality

### Admin Features
- ✅ Admin Dashboard
- ✅ Product Management (CRUD)
- ✅ Order Management
- ✅ User Management
- ✅ Sales Analytics
- ✅ Inventory Tracking
- ✅ Category Management

### Technical Features
- ✅ Responsive Design (Mobile-First)
- ✅ Real-time Notifications
- ✅ Image Upload & Optimization
- ✅ Search & Filtering
- ✅ Pagination
- ✅ Email Notifications
- ✅ Payment Gateway Integration
- ✅ JWT Authentication
- ✅ API Rate Limiting
- ✅ Data Validation

## 🛠️ Tech Stack

### Frontend
- **Framework**: React 18.2.0 with TypeScript
- **Styling**: Tailwind CSS + Material-UI
- **State Management**: Redux Toolkit + RTK Query
- **Routing**: React Router v6
- **Form Handling**: React Hook Form + Yup validation
- **HTTP Client**: Axios with interceptors

### Backend
- **Runtime**: Node.js 18+
- **Framework**: Express.js with TypeScript
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JWT + bcrypt
- **File Upload**: Cloudinary
- **Payment**: Stripe API
- **Email**: Nodemailer + SendGrid

### DevOps & Tools
- **Containerization**: Docker & Docker Compose
- **Deployment**: Frontend (Vercel), Backend (Railway)
- **CI/CD**: GitHub Actions
- **Testing**: Jest, React Testing Library, Supertest
- **Code Quality**: ESLint, Prettier, Husky
- **Monitoring**: Morgan logging

## 📸 Screenshots

### Homepage
![Homepage](screenshots/homepage.png)
*Modern, responsive homepage with featured products and categories*

### Product Details
![Product Details](screenshots/product-details.png)
*Detailed product view with reviews, ratings, and add to cart functionality*

### Shopping Cart
![Shopping Cart](screenshots/shopping-cart.png)
*Interactive shopping cart with quantity management and checkout options*

### Admin Dashboard
![Admin Dashboard](screenshots/admin-dashboard.png)
*Comprehensive admin panel with sales analytics and management tools*

### Mobile View
![Mobile View](screenshots/mobile-responsive.png)
*Fully responsive design optimized for mobile devices*

## 🔗 Live Demo

- **Frontend**: [https://mohit-ecommerce.vercel.app](https://mohit-ecommerce.vercel.app)
- **Admin Panel**: [https://mohit-ecommerce.vercel.app/admin](https://mohit-ecommerce.vercel.app/admin)
- **API Documentation**: [https://mohit-ecommerce-api.railway.app/api/docs](https://mohit-ecommerce-api.railway.app/api/docs)

### Demo Credentials
```
Customer Account:
Email: demo@customer.com
Password: Demo123!

Admin Account:
Email: admin@mohit.com
Password: Admin123!
```

## 🏗️ Architecture Overview

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   React Client  │────│   Express API   │────│   MongoDB       │
│   (Frontend)    │    │   (Backend)     │    │   (Database)    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
    ┌─────────┐            ┌─────────┐            ┌─────────┐
    │ Vercel  │            │Railway  │            │MongoDB  │
    │Hosting  │            │Hosting  │            │ Atlas   │
    └─────────┘            └─────────┘            └─────────┘
```

## 📊 Performance Metrics

- **Lighthouse Score**: 95+ (Performance, Accessibility, Best Practices, SEO)
- **Bundle Size**: <500KB (gzipped)
- **API Response Time**: <200ms average
- **Database Queries**: Optimized with indexing
- **Image Loading**: Lazy loading + WebP format

## 🚦 Getting Started

### Quick Start (Docker)
```bash
# Clone the repository
git clone https://github.com/mohit/ecommerce-platform.git
cd ecommerce-platform

# Start with Docker Compose
docker-compose up -d

# Access the application
# Frontend: http://localhost:3000
# Backend: http://localhost:5000
# MongoDB: localhost:27017
```

### Manual Setup
For detailed manual setup instructions, see [SETUP.md](SETUP.md)

## 📚 Documentation

- 📋 **[Setup Instructions](SETUP.md)** - Complete installation and configuration guide
- 🛠️ **[Tech Stack Details](TECH_STACK.md)** - Detailed technology explanations
- ⭐ **[Features Overview](FEATURES.md)** - Comprehensive feature breakdown
- 🚀 **[Deployment Guide](DEPLOYMENT.md)** - Step-by-step deployment instructions
- 🔧 **[API Documentation](API.md)** - Complete API reference
- 🐛 **[Troubleshooting](TROUBLESHOOTING.md)** - Common issues and solutions

## 🧪 Testing

```bash
# Run all tests
npm test

# Run frontend tests
cd frontend && npm test

# Run backend tests
cd backend && npm test

# Run e2e tests
npm run test:e2e

# Generate coverage report
npm run test:coverage
```

## 🔒 Security Features

- **Authentication**: JWT-based authentication with refresh tokens
- **Authorization**: Role-based access control (Customer, Admin)
- **Data Validation**: Input sanitization and validation on both client and server
- **Rate Limiting**: API rate limiting to prevent abuse
- **CORS**: Configured Cross-Origin Resource Sharing
- **Helmet**: Security headers for Express.js
- **Password Security**: bcrypt hashing with salt rounds
- **Environment Variables**: Sensitive data stored securely

## 🌟 Learning Outcomes

After studying this project, you'll understand:

### Frontend Development
- Modern React patterns and hooks
- State management with Redux Toolkit
- TypeScript in React applications
- Responsive design with Tailwind CSS
- Form handling and validation
- API integration and error handling

### Backend Development
- RESTful API design principles
- Authentication and authorization
- Database design and relationships
- File upload and cloud storage
- Payment gateway integration
- Email service integration

### DevOps & Deployment
- Docker containerization
- CI/CD pipeline setup
- Environment configuration
- Database hosting and management
- Frontend and backend deployment
- Monitoring and logging

## 🤝 Contributing

We welcome contributions! Please read our [Contributing Guidelines](../../CONTRIBUTING.md) for details on:
- Setting up the development environment
- Code style and standards
- Pull request process
- Issue reporting

### Development Setup
```bash
# Fork and clone the repository
git clone https://github.com/YOUR_USERNAME/Cool-Projects-Collections.git

# Navigate to this project
cd projects/mohit-ecommerce-platform

# Follow the setup instructions in SETUP.md
```

## 📈 Future Enhancements

- 📱 **Mobile App**: React Native mobile application
- 🤖 **AI Recommendations**: Machine learning-based product recommendations
- 💬 **Live Chat**: Real-time customer support chat
- 🌐 **Multi-language**: Internationalization support
- 📊 **Advanced Analytics**: Enhanced business intelligence dashboard
- 🔔 **Push Notifications**: Real-time notifications for orders and promotions
- 🎨 **Theme Customization**: Dark mode and custom themes
- 🔍 **Advanced Search**: Elasticsearch integration for better search

## 👨‍💻 About the Developer

**Mohit** - Full Stack Developer passionate about creating scalable web applications

- 🌐 **Portfolio**: [mohit-portfolio.dev](https://mohit-portfolio.dev)
- 💼 **LinkedIn**: [linkedin.com/in/mohit-dev](https://linkedin.com/in/mohit-dev)
- 🐦 **Twitter**: [@mohit_codes](https://twitter.com/mohit_codes)
- 📧 **Email**: mohit@developer.com

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](../../LICENSE) file for details.

## 🙏 Acknowledgments

- **Design Inspiration**: Shopify, Amazon, and modern e-commerce platforms
- **Icons**: Heroicons and Lucide React
- **Images**: Unsplash and custom photography
- **Community**: Thanks to all contributors and the open-source community

---

<div align="center">

**⭐ If you found this project helpful, please give it a star! ⭐**

**[🔗 View Live Demo](https://mohit-ecommerce.vercel.app)** | **[📖 Read Documentation](SETUP.md)** | **[🤝 Contribute](../../CONTRIBUTING.md)**

*Built with ❤️ by Mohit and the open-source community*

</div>
