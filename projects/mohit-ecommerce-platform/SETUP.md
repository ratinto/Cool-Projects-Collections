# 🚀 Setup Instructions

This guide will help you set up the Mohit E-Commerce Platform on your local development environment.

## 📋 Prerequisites

Before you begin, ensure you have the following installed on your system:

### Required Software
- **Node.js** (v18.17+ LTS) - [Download here](https://nodejs.org/)
- **npm** (v9+) or **yarn** (v1.22+) - Package manager
- **Git** (v2.34+) - Version control
- **MongoDB** (v6.0+) - Database
  - Option 1: [MongoDB Community Server](https://www.mongodb.com/try/download/community) (Local)
  - Option 2: [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) (Cloud)

### Optional but Recommended
- **Docker** (v24.0+) - For containerized development
- **Docker Compose** (v2.20+) - Multi-container orchestration
- **MongoDB Compass** - GUI for MongoDB
- **Postman** or **Insomnia** - API testing
- **VSCode** - Code editor with extensions

### VSCode Extensions (Recommended)
```
- ES7+ React/Redux/React-Native snippets
- TypeScript Importer
- Tailwind CSS IntelliSense
- Prettier - Code formatter
- ESLint
- Thunder Client (API testing)
- GitLens
- Auto Rename Tag
- Bracket Pair Colorizer
```

## 🛠️ Installation Methods

Choose one of the following installation methods:

### Method 1: Docker Setup (Recommended for Quick Start)

1. **Clone the Repository**
   ```bash
   git clone https://github.com/mohit/ecommerce-platform.git
   cd ecommerce-platform
   ```

2. **Environment Setup**
   ```bash
   # Copy environment files
   cp .env.example .env
   cp frontend/.env.example frontend/.env
   cp backend/.env.example backend/.env
   ```

3. **Start with Docker Compose**
   ```bash
   # Build and start all services
   docker-compose up -d

   # View logs
   docker-compose logs -f

   # Stop services
   docker-compose down
   ```

4. **Access the Application**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:5000
   - MongoDB: localhost:27017

### Method 2: Manual Setup (For Development)

#### Step 1: Clone and Setup Repository
```bash
# Clone the repository
git clone https://github.com/mohit/ecommerce-platform.git
cd ecommerce-platform

# Install root dependencies (if any)
npm install
```

#### Step 2: Backend Setup

```bash
# Navigate to backend directory
cd backend

# Install dependencies
npm install

# Copy environment file
cp .env.example .env
```

**Configure Backend Environment Variables:**
Edit `backend/.env` file:
```bash
# Server Configuration
NODE_ENV=development
PORT=5000
CLIENT_URL=http://localhost:3000

# Database
MONGODB_URI=mongodb://localhost:27017/ecommerce_dev
# OR for MongoDB Atlas:
# MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/ecommerce_dev

# JWT Configuration
JWT_SECRET=your_super_secret_jwt_key_min_32_chars
JWT_EXPIRE=7d
JWT_REFRESH_SECRET=your_refresh_token_secret
JWT_REFRESH_EXPIRE=30d

# Cloudinary (Image Upload)
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# Stripe Payment
STRIPE_SECRET_KEY=sk_test_your_stripe_secret_key
STRIPE_WEBHOOK_SECRET=whsec_your_webhook_secret

# Email Service (SendGrid)
SENDGRID_API_KEY=SG.your_sendgrid_api_key
FROM_EMAIL=noreply@yourdomain.com

# Admin User (Optional - for seeding)
ADMIN_EMAIL=admin@mohit.com
ADMIN_PASSWORD=Admin123!
```

**Start Backend Server:**
```bash
# Development mode with hot reload
npm run dev

# Or production mode
npm start

# Run with specific port
PORT=8000 npm run dev
```

#### Step 3: Frontend Setup

```bash
# Navigate to frontend directory (in new terminal)
cd frontend

# Install dependencies
npm install

# Copy environment file
cp .env.example .env
```

**Configure Frontend Environment Variables:**
Edit `frontend/.env` file:
```bash
# API Configuration
REACT_APP_API_URL=http://localhost:5000/api
REACT_APP_SOCKET_URL=http://localhost:5000

# Stripe (Public Key)
REACT_APP_STRIPE_PUBLISHABLE_KEY=pk_test_your_stripe_publishable_key

# Google Analytics (Optional)
REACT_APP_GA_TRACKING_ID=G-XXXXXXXXXX

# App Configuration
REACT_APP_APP_NAME=Mohit E-Commerce
REACT_APP_APP_VERSION=1.0.0
```

**Start Frontend Server:**
```bash
# Development mode
npm start

# Or with specific port
PORT=3001 npm start

# Build for production
npm run build
```

#### Step 4: Database Setup

**Option A: Local MongoDB**
```bash
# Start MongoDB service
# On macOS with Homebrew:
brew services start mongodb-community

# On Ubuntu:
sudo systemctl start mongod

# On Windows:
net start MongoDB
```

**Option B: MongoDB Atlas (Cloud)**
1. Create account at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a new cluster
3. Get connection string
4. Update `MONGODB_URI` in backend `.env`

**Seed Database (Optional):**
```bash
# Navigate to backend directory
cd backend

# Seed with sample data
npm run seed

# Or seed specific data
npm run seed:users
npm run seed:products
npm run seed:categories
```

## 🔧 Additional Configuration

### Cloudinary Setup (Image Upload)
1. Create account at [Cloudinary](https://cloudinary.com/)
2. Get your cloud name, API key, and API secret
3. Update environment variables in backend `.env`

### Stripe Setup (Payment Processing)
1. Create account at [Stripe](https://stripe.com/)
2. Get test API keys from dashboard
3. Update environment variables in both frontend and backend `.env`
4. Set up webhook endpoint: `http://localhost:5000/api/payments/webhook`

### SendGrid Setup (Email Service)
1. Create account at [SendGrid](https://sendgrid.com/)
2. Create API key with full access
3. Update `SENDGRID_API_KEY` in backend `.env`
4. Verify sender email address

## 🧪 Running Tests

### Backend Tests
```bash
cd backend

# Run all tests
npm test

# Run tests in watch mode
npm run test:watch

# Run tests with coverage
npm run test:coverage

# Run specific test file
npm test -- auth.test.js
```

### Frontend Tests
```bash
cd frontend

# Run all tests
npm test

# Run tests in watch mode
npm test -- --watch

# Run tests with coverage
npm test -- --coverage

# Run e2e tests
npm run test:e2e
```

## 🔍 Verification Steps

### 1. Check Backend Health
```bash
# Test API endpoint
curl http://localhost:5000/api/health

# Should return: {"status": "OK", "timestamp": "..."}
```

### 2. Check Database Connection
```bash
# Check MongoDB connection
curl http://localhost:5000/api/health/db

# Should return: {"status": "Connected", "database": "ecommerce_dev"}
```

### 3. Check Frontend
- Navigate to http://localhost:3000
- Verify homepage loads
- Check console for errors
- Test navigation between pages

### 4. Test API Integration
- Try user registration
- Test login functionality
- Browse products
- Add items to cart

## 🐛 Troubleshooting

### Common Issues

#### MongoDB Connection Error
```bash
Error: connect ECONNREFUSED 127.0.0.1:27017
```
**Solution:**
- Ensure MongoDB is running
- Check MongoDB service status
- Verify connection string in `.env`

#### Port Already in Use
```bash
Error: listen EADDRINUSE :::3000
```
**Solution:**
```bash
# Find and kill process using port
lsof -ti:3000 | xargs kill -9

# Or use different port
PORT=3001 npm start
```

#### Environment Variables Not Loading
**Solution:**
- Ensure `.env` files are in correct directories
- Restart development servers after changing `.env`
- Check file names (should be `.env`, not `.env.txt`)

#### CORS Errors
```bash
Access to fetch at 'http://localhost:5000/api/...' from origin 'http://localhost:3000' has been blocked by CORS policy
```
**Solution:**
- Check `CLIENT_URL` in backend `.env`
- Ensure CORS is configured correctly in backend
- Restart backend server

#### Dependency Installation Errors
```bash
npm ERR! peer dep missing
```
**Solution:**
```bash
# Clear npm cache
npm cache clean --force

# Delete node_modules and reinstall
rm -rf node_modules package-lock.json
npm install

# Or use legacy peer deps
npm install --legacy-peer-deps
```

### Database Issues

#### MongoDB Won't Start
**Solution:**
```bash
# Check MongoDB status
brew services list | grep mongodb

# Restart MongoDB
brew services restart mongodb-community

# Check MongoDB logs
tail -f /usr/local/var/log/mongodb/mongo.log
```

#### Database Permission Errors
**Solution:**
```bash
# Fix MongoDB permissions (macOS)
sudo chown -R $(whoami) /usr/local/var/mongodb
sudo chown -R $(whoami) /usr/local/var/log/mongodb
```

### Performance Issues

#### Slow Database Queries
**Solution:**
- Check database indexes
- Use MongoDB Compass to analyze queries
- Enable slow query logging

#### Large Bundle Size
**Solution:**
```bash
# Analyze bundle size
cd frontend
npm run build
npm run analyze

# Optimize imports
# Use tree shaking
# Implement code splitting
```

## 📊 Development Tools

### Database Management
```bash
# MongoDB Compass GUI
# Download from: https://www.mongodb.com/products/compass

# Command line tools
mongosh # MongoDB Shell
mongostat # Statistics
mongotop # Collection activity
```

### API Testing
```bash
# Using curl
curl -X GET http://localhost:5000/api/products

# Using httpie
http GET localhost:5000/api/products

# Import Postman collection
# File: docs/postman-collection.json
```

### Code Quality
```bash
# Run linter
npm run lint

# Fix linting issues
npm run lint:fix

# Format code
npm run format

# Type checking (TypeScript)
npm run type-check
```

## 📚 Next Steps

After successful setup:

1. **Explore the Codebase**
   - Review project structure
   - Understand component architecture
   - Study API endpoints

2. **Customize the Application**
   - Modify branding and colors
   - Add new features
   - Update product categories

3. **Deploy to Production**
   - Follow [DEPLOYMENT.md](DEPLOYMENT.md) guide
   - Configure production environment
   - Set up monitoring and logging

4. **Contribute to the Project**
   - Read [CONTRIBUTING.md](../../CONTRIBUTING.md)
   - Find issues to work on
   - Submit pull requests

## 🆘 Getting Help

If you encounter issues not covered in this guide:

1. **Check the Documentation**
   - [API Documentation](API.md)
   - [Troubleshooting Guide](TROUBLESHOOTING.md)
   - [Deployment Guide](DEPLOYMENT.md)

2. **Community Support**
   - Create an issue on GitHub
   - Join our Discord community
   - Check Stack Overflow

3. **Contact Information**
   - Email: support@mohit-ecommerce.com
   - GitHub Issues: [Create Issue](https://github.com/mohit/ecommerce-platform/issues)

---

**🎉 Congratulations! You've successfully set up the Mohit E-Commerce Platform. Happy coding!**
