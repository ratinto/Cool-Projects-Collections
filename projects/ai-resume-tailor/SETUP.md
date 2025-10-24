# 🚀 Setup Instructions

Want to run this locally? Here's how. The Python backend can be a bit tricky to set up, but once it's running it's smooth sailing.

## 📋 Prerequisites

You'll need:
- **Node.js**: 18+ ([Download](https://nodejs.org/)) - I'm using 18.17.0
- **Python**: 3.10+ ([Download](https://www.python.org/downloads/)) - Using 3.11.0
- **OpenAI API Key**: Sign up at [OpenAI Platform](https://platform.openai.com/) - billing required
- **Git**: Probably already have this

### Optional
- **Python Virtual Environment**: Makes dependency management easier
- **Postman**: For testing the API

## 🔧 Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/ai-resume-tailor.git
cd ai-resume-tailor
```

### 2. Set Up Backend

```bash
# Navigate to backend
cd backend

# Create virtual environment (recommended)
python -m venv venv

# Activate virtual environment
# On macOS/Linux:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Create environment file
cp .env.example .env
```

### 3. Configure Backend Environment

Edit the `.env` file in the backend directory:

```env
# Server Configuration
PORT=5000
ENVIRONMENT=development

# OpenAI API Key (REQUIRED)
OPENAI_API_KEY=your-openai-api-key-here

# CORS Configuration
FRONTEND_URL=http://localhost:3000

# File Upload Limits
MAX_FILE_SIZE=10485760  # 10MB
ALLOWED_EXTENSIONS=pdf,docx,doc
```

**Important:** Without the OpenAI API key, nothing will work!

### 4. Set Up Frontend

```bash
# Navigate to frontend
cd ../frontend

# Install dependencies
npm install

# Create environment file
cp .env.example .env
```

Edit the `.env` file in the frontend directory:

```env
# API Configuration
REACT_APP_API_URL=http://localhost:5000/api
```

### 5. Download spaCy Model

The backend needs a spaCy model for text processing:

```bash
cd backend

# Download the English model
python -m spacy download en_core_web_sm
```

This downloads a ~13MB model for text analysis.

### 6. Start the Application

#### Start Backend

```bash
# Make sure you're in the backend directory
cd backend

# Make sure virtual environment is activated
source venv/bin/activate  # macOS/Linux
# or
venv\Scripts\activate  # Windows

# Start the server
python app.py
# or
uvicorn app:app --reload

# Should start on http://localhost:5000
```

#### Start Frontend

```bash
# Open a new terminal
cd frontend

# Start development server
npm start

# Should open on http://localhost:3000
```

## 🐳 Docker Setup (Alternative)

### Using Docker Compose

```bash
# From project root
docker-compose up -d

# Check logs
docker-compose logs -f

# Stop containers
docker-compose down
```

### Dockerfile Backend

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN python -m spacy download en_core_web_sm

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "5000"]
```

## 🧪 Testing

### Backend Tests

```bash
cd backend

# Run all tests
pytest

# Run with coverage
pytest --cov=app

# Run specific test file
pytest tests/test_resume_parser.py
```

### Frontend Tests

```bash
cd frontend

# Run tests
npm test

# Run with coverage
npm test -- --coverage
```

## 📝 API Endpoints

### Main Endpoints

```
POST   /api/upload-resume    - Upload resume file
POST   /api/analyze          - Analyze resume against job description
POST   /api/optimize         - Optimize resume
GET    /api/health           - Health check
```

### Example Usage

```bash
# Upload resume
curl -X POST http://localhost:5000/api/upload-resume \
  -F "file=@resume.pdf"

# Analyze
curl -X POST http://localhost:5000/api/analyze \
  -H "Content-Type: application/json" \
  -d '{"resume_text": "...", "job_description": "..."}'
```

## 🔍 Verification

### Check Backend

1. Visit `http://localhost:5000/api/health`
2. Should return: `{"status": "ok"}`

### Check Frontend

1. Visit `http://localhost:3000`
2. Should see the upload interface

### Test Resume Upload

1. Go to the app
2. Upload a sample resume PDF
3. Paste a job description
4. Click "Optimize"
5. Should see AI suggestions appear

## 🐛 Troubleshooting

### Backend Won't Start

**Issue:** Python import errors
```bash
# Make sure virtual environment is activated
source venv/bin/activate

# Reinstall dependencies
pip install -r requirements.txt
```

**Issue:** Port already in use
```bash
# Find what's using port 5000
lsof -i :5000

# Kill it
kill -9 <PID>
```

### Frontend Can't Connect to Backend

**Check:**
- Backend is running on port 5000
- CORS is configured correctly
- `REACT_APP_API_URL` in frontend `.env` is correct

### OpenAI API Errors

**Things to check:**
- API key is correct (no extra spaces)
- You have credits in your OpenAI account
- Rate limits not exceeded
- Billing is enabled

**Common error:** "Insufficient quota" - means you ran out of credits.

### PDF Parsing Issues

PDF parsing can be finicky:
- Some PDFs are scanned images (no text) - won't work
- Complex layouts might lose formatting
- Test with simple PDFs first

### File Upload Errors

**Issue:** File too large
- Default limit is 10MB
- Increase `MAX_FILE_SIZE` in backend `.env`

**Issue:** Invalid file type
- Only PDF, DOCX, DOC are supported
- Check `ALLOWED_EXTENSIONS` in config

## 🔐 Security Notes

1. **Never commit `.env` files** - Already in `.gitignore`
2. **Keep OpenAI API key secret** - It's worth money!
3. **Validate file uploads** - Check file types and sizes
4. **Use HTTPS in production** - Don't skip this
5. **Limit API rate** - Add rate limiting for production

## 📚 Next Steps

If everything is working:
1. Read [FEATURES.md](FEATURES.md) to understand features
2. Check [TECH_STACK.md](TECH_STACK.md) for tech details
3. Try uploading different resume formats
4. Test with various job descriptions
5. Tweak the AI prompts for better results

## ✅ Setup Checklist

- [ ] Python 3.10+ installed
- [ ] Node.js 18+ installed
- [ ] Virtual environment created and activated
- [ ] Backend dependencies installed
- [ ] Frontend dependencies installed
- [ ] spaCy model downloaded
- [ ] OpenAI API key configured
- [ ] Backend server running
- [ ] Frontend server running
- [ ] Can upload resume
- [ ] AI optimization works

If you checked all these, you're all set! 🎉

---

Questions? Open a GitHub issue!

Good luck with your job applications! 🚀

