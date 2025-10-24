# 📄 AI Resume Tailor

Tired of spending hours tweaking your resume for every single job application? Yeah, me too. That's why I built this - an AI-powered web app that automatically customizes your resume for any job posting. Just upload your resume, paste the job description, and let the AI figure out what skills to highlight and how to phrase things better for that ATS score.

## 🚀 Features

### Core Features
- ✅ **Resume Upload**: Upload your existing resume (PDF, DOCX, or DOC)
- ✅ **Job Description Input**: Paste the job description and let AI analyze it
- ✅ **AI Matching**: Automatically matches keywords and identifies relevant skills
- ✅ **Smart Rewriting**: AI rewrites sections to better fit the job description
- ✅ **ATS Optimization**: Suggests bullet points and phrasing to improve ATS compatibility
- ✅ **Export Options**: Download optimized resume as PDF or DOCX
- ✅ **Score Preview**: See your estimated ATS score before and after optimization

### Advanced Features
- ✅ Multiple Resume Templates
- ✅ Keyword Analysis Dashboard
- ✅ Skill Gap Identification
- ✅ Resume Version History
- ✅ Comparison View (before/after)

## 🛠️ Tech Stack

### Frontend
- **Framework**: React.js
- **Styling**: Tailwind CSS + Headless UI
- **State Management**: Zustand
- **PDF Handling**: react-pdf
- **File Upload**: react-dropzone

### Backend
- **Runtime**: Python 3.10+
- **Framework**: Flask/FastAPI
- **AI Integration**: OpenAI API
- **PDF Processing**: PyPDF2, python-docx
- **Text Analysis**: spaCy

### DevOps & Tools
- **Containerization**: Docker
- **Deployment**: Frontend (Vercel), Backend (Railway/Render)
- **Testing**: Jest, Pytest
- **Code Quality**: ESLint, Black

## 📸 Screenshots

### Dashboard
![Dashboard](screenshots/dashboard.png)
*Clean interface for uploading resume and pasting job description*

### Optimization Results
![Results](screenshots/results.png)
*Before/after comparison showing ATS score improvement*

### Resume Editor
![Editor](screenshots/editor.png)
*AI-suggested improvements highlighted in the resume*

### Export Options
![Export](screenshots/export.png)
*Multiple export formats available*

## 🎯 Why I Built This

Honestly? I was applying to jobs and spending way too much time customizing my resume for each position. So I thought - what if AI could do this automatically? This app analyzes job descriptions and optimizes your resume to match what employers are looking for.

Here's what makes it useful:
- Saves hours of manual resume editing
- Improves ATS compatibility (most resumes never even get seen by humans)
- Highlights the right skills automatically
- Suggests better phrasing and bullet points
- Actually works (tested it with real job applications)

## 🏗️ Architecture Overview

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   React Client  │────│   Flask API     │────│   OpenAI API    │
│   (Frontend)    │    │   (Backend)     │    │   (AI Service)  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
    ┌─────────┐            ┌─────────┐            ┌─────────┐
    │ Vercel  │            │Railway  │            │ OpenAI  │
    │Hosting  │            │Hosting  │            │   API   │
    └─────────┘            └─────────┘            └─────────┘
```

## 🚦 Getting Started

### Prerequisites
You'll need:
- Node.js 18+ (for frontend)
- Python 3.10+ (for backend)
- OpenAI API Key (unfortunately requires billing)
- Git

### Quick Start
```bash
# Clone the repo
git clone https://github.com/your-username/ai-resume-tailor.git
cd ai-resume-tailor

# Set up backend
cd backend
pip install -r requirements.txt
cp .env.example .env
# Add your OpenAI API key to .env

# Set up frontend
cd ../frontend
npm install
cp .env.example .env

# Run both
# Terminal 1:
cd backend && python app.py

# Terminal 2:
cd frontend && npm start
```

**Note:** Make sure your OpenAI API key is set up correctly or the optimization won't work.

## 🎨 Difficulty Level

**Intermediate** - Not too hard, but not trivial either.

Here's what you'll need to handle:
- File parsing (PDFs and Word docs can be annoying)
- AI prompt engineering (getting good results from OpenAI takes iteration)
- Text extraction and analysis
- Resume formatting without breaking the layout
- ATS scoring algorithm (this part is tricky)

I'd say the hardest part is making sure the AI doesn't mess up your resume formatting while rewriting it.

## 🚀 Future Ideas

Here's what I'd like to add next:
- 🔗 **LinkedIn Integration**: Scrape job descriptions directly from LinkedIn
- 📑 **Template Library**: Pre-built resume templates for different industries
- 📊 **Format Support**: Academic resumes, tech resumes, business resumes - different formats
- 🤖 **Cover Letter Generator**: AI writes matching cover letters too
- 📈 **Analytics**: Track which resumes got callbacks
- 💬 **Interview Prep**: Generate potential interview questions based on the job
- 🌐 **Multi-language**: Support for resumes in different languages

Let me know if you have other ideas!

## 🌟 What You'll Learn

Building this taught me:
- How to parse and manipulate PDF and Word documents
- AI prompt engineering for better results
- ATS systems and what they look for
- Text analysis and keyword extraction
- File format conversions

**Pro tip:** Start with PDF parsing - it's the most painful part to get right.

## 🤝 Contributing

Contributions welcome! Check out [CONTRIBUTING.md](../../CONTRIBUTING.md) for details.

I'm especially interested in:
- Better ATS scoring algorithms
- Resume template designs
- Performance optimizations
- More AI prompt improvements

## 📄 License

MIT License - see [LICENSE](../../LICENSE) for details.

---

**Contributed by @yats0x7 for Hacktoberfest 2025**

<div align="center">

**⭐ Found this helpful? Give it a star! ⭐**

Made for Hacktoberfest 2025

</div>

