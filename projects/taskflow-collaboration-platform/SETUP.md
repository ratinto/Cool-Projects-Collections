# 🚀 Setup Instructions

This guide will help you set up the TaskFlow Collaboration Platform on your local development environment.

## 📋 Prerequisites

Before you begin, ensure you have the following installed on your system:

### Required Software
- **Node.js** (v18.17+ LTS) - [Download here](https://nodejs.org/)
- **npm** (v9+) or **yarn** (v1.22+) - Package manager
- **Git** (v2.34+) - Version control
- **PostgreSQL** (v15+) - Database
  - Option 1: [PostgreSQL Community](https://www.postgresql.org/download/) (Local)
  - Option 2: [Supabase](https://supabase.com/) (Cloud)
- **Redis** (v7.0+) - Caching and sessions
  - Option 1: [Redis Community](https://redis.io/download) (Local)
  - Option 2: [Redis Cloud](https://redis.com/redis-enterprise-cloud/overview/) (Cloud)

### Optional but Recommended
- **Docker** (v24.0+) - For containerized development
- **Docker Compose** (v2.20+) - Multi-container orchestration
- **pgAdmin** - GUI for PostgreSQL
- **RedisInsight** - GUI for Redis
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
- Prisma
- PostgreSQL
```

## 🛠️ Installation Methods

Choose one of the following installation methods:

### Method 1: Docker Setup (Recommended for Quick Start)

1. **Clone the Repository**
   ```bash
   git clone https://github.com/taskflow/collaboration-platform.git
   cd collaboration-platform
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
   - PostgreSQL: localhost:5432
   - Redis: localhost:6379

### Method 2: Manual Setup (For Development)

#### Step 1: Clone and Setup Repository
```bash
# Clone the repository
git clone https://github.com/taskflow/collaboration-platform.git
cd collaboration-platform

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
DATABASE_URL=postgresql://username:password@localhost:5432/taskflow_dev
# OR for Supabase:
# DATABASE_URL=postgresql://postgres:[password]@db.[project-ref].supabase.co:5432/postgres

# Redis Configuration
REDIS_URL=redis://localhost:6379
# OR for Redis Cloud:
# REDIS_URL=redis://username:password@host:port

# JWT Configuration
JWT_SECRET=your_super_secret_jwt_key_min_32_chars
JWT_EXPIRE=7d
JWT_REFRESH_SECRET=your_refresh_token_secret
JWT_REFRESH_EXPIRE=30d

# AWS S3 (File Storage)
AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
AWS_S3_BUCKET=taskflow-dev
AWS_REGION=us-east-1

# Email Service (SendGrid)
SENDGRID_API_KEY=SG.your_sendgrid_api_key
FROM_EMAIL=noreply@taskflow.dev

# Admin User (Optional - for seeding)
ADMIN_EMAIL=admin@taskflow.com
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
NEXT_PUBLIC_API_URL=http://localhost:5000/api
NEXT_PUBLIC_SOCKET_URL=http://localhost:5000

# AWS S3 (Public URLs)
NEXT_PUBLIC_AWS_S3_BUCKET=taskflow-dev
NEXT_PUBLIC_AWS_REGION=us-east-1

# Google Analytics (Optional)
NEXT_PUBLIC_GA_TRACKING_ID=G-XXXXXXXXXX

# App Configuration
NEXT_PUBLIC_APP_NAME=TaskFlow
NEXT_PUBLIC_APP_VERSION=1.0.0
```

**Start Frontend Server:**
```bash
# Development mode
npm run dev

# Or with specific port
PORT=3001 npm run dev

# Build for production
npm run build
```

#### Step 4: Database Setup

**Option A: Local PostgreSQL**
```bash
# Install PostgreSQL (macOS with Homebrew)
brew install postgresql
brew services start postgresql

# Create database
createdb taskflow_dev

# Connect to database
psql taskflow_dev
```

**Option B: Supabase (Cloud)**
1. Create account at [Supabase](https://supabase.com/)
2. Create a new project
3. Get connection string from Settings > Database
4. Update `DATABASE_URL` in backend `.env`

**Run Database Migrations:**
```bash
# Navigate to backend directory
cd backend

# Generate Prisma client
npx prisma generate

# Run migrations
npx prisma migrate dev

# Seed with sample data
npm run seed

# Or seed specific data
npm run seed:users
npm run seed:teams
npm run seed:projects
```

#### Step 5: Redis Setup

**Option A: Local Redis**
```bash
# Install Redis (macOS with Homebrew)
brew install redis
brew services start redis

# Test Redis connection
redis-cli ping
```

**Option B: Redis Cloud**
1. Create account at [Redis Cloud](https://redis.com/)
2. Create a new database
3. Get connection string
4. Update `REDIS_URL` in backend `.env`

## 🔧 Additional Configuration

### AWS S3 Setup (File Storage)
1. Create AWS account and S3 bucket
2. Create IAM user with S3 permissions
3. Get access key and secret key
4. Update environment variables in backend `.env`

### SendGrid Setup (Email Service)
1. Create account at [SendGrid](https://sendgrid.com/)
2. Create API key with full access
3. Update `SENDGRID_API_KEY` in backend `.env`
4. Verify sender email address

### Socket.io Setup (Real-time)
Socket.io is automatically configured with the backend. No additional setup required.

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
# Check PostgreSQL connection
curl http://localhost:5000/api/health/db

# Should return: {"status": "Connected", "database": "taskflow_dev"}
```

### 3. Check Redis Connection
```bash
# Check Redis connection
curl http://localhost:5000/api/health/redis

# Should return: {"status": "Connected", "redis": "ready"}
```

### 4. Check Frontend
- Navigate to http://localhost:3000
- Verify homepage loads
- Check console for errors
- Test navigation between pages

### 5. Test API Integration
- Try user registration
- Test login functionality
- Create a team
- Create a project
- Add tasks

## 🐛 Troubleshooting

### Common Issues

#### PostgreSQL Connection Error
```bash
Error: connect ECONNREFUSED 127.0.0.1:5432
```
**Solution:**
- Ensure PostgreSQL is running
- Check PostgreSQL service status
- Verify connection string in `.env`
- Check if database exists

#### Redis Connection Error
```bash
Error: connect ECONNREFUSED 127.0.0.1:6379
```
**Solution:**
- Ensure Redis is running
- Check Redis service status
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
PORT=3001 npm run dev
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

#### Database Migration Errors
```bash
Error: P1001: Can't reach database server
```
**Solution:**
- Check database connection string
- Ensure database server is running
- Verify database credentials
- Check network connectivity

#### Prisma Client Errors
```bash
Error: PrismaClient is unable to run
```
**Solution:**
```bash
# Regenerate Prisma client
npx prisma generate

# Reset database
npx prisma migrate reset

# Deploy migrations
npx prisma migrate deploy
```

### Database Issues

#### PostgreSQL Won't Start
**Solution:**
```bash
# Check PostgreSQL status
brew services list | grep postgresql

# Restart PostgreSQL
brew services restart postgresql

# Check PostgreSQL logs
tail -f /usr/local/var/log/postgresql.log
```

#### Database Permission Errors
**Solution:**
```bash
# Fix PostgreSQL permissions (macOS)
sudo chown -R $(whoami) /usr/local/var/postgres

# Create database user
createuser -s taskflow_user
```

#### Redis Won't Start
**Solution:**
```bash
# Check Redis status
brew services list | grep redis

# Restart Redis
brew services restart redis

# Check Redis logs
tail -f /usr/local/var/log/redis.log
```

### Performance Issues

#### Slow Database Queries
**Solution:**
- Check database indexes
- Use Prisma query optimization
- Enable slow query logging
- Analyze query performance

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

#### Memory Issues
**Solution:**
- Check for memory leaks
- Optimize database queries
- Implement proper caching
- Monitor memory usage

## 📊 Development Tools

### Database Management
```bash
# PostgreSQL command line tools
psql taskflow_dev # PostgreSQL Shell
pg_dump taskflow_dev > backup.sql # Database backup
pg_restore -d taskflow_dev backup.sql # Database restore

# Prisma Studio (GUI)
npx prisma studio
```

### Redis Management
```bash
# Redis command line tools
redis-cli # Redis Shell
redis-cli monitor # Monitor Redis commands
redis-cli info # Redis information
```

### API Testing
```bash
# Using curl
curl -X GET http://localhost:5000/api/teams

# Using httpie
http GET localhost:5000/api/teams

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

# Database schema validation
npx prisma validate
```

## 📚 Next Steps

After successful setup:

1. **Explore the Codebase**
   - Review project structure
   - Understand component architecture
   - Study API endpoints
   - Learn database schema

2. **Customize the Application**
   - Modify branding and colors
   - Add new features
   - Update team settings
   - Customize task templates

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
   - Email: support@taskflow.dev
   - GitHub Issues: [Create Issue](https://github.com/taskflow/collaboration-platform/issues)

---

**🎉 Congratulations! You've successfully set up the TaskFlow Collaboration Platform. Happy coding!**
