# 💻 Code Snippets

Important code examples from the AI Resume Tailor project.

## 📁 Folder Structure

```
code-snippets/
├── README.md (this file)
├── backend/
│   ├── app.py (FastAPI main app)
│   ├── resume_parser.py (PDF/DOCX parsing)
│   ├── ai_service.py (OpenAI integration)
│   └── ats_scorer.py (ATS scoring logic)
├── frontend/
│   ├── components/
│   │   ├── ResumeUpload.jsx (File upload component)
│   │   ├── JobDescriptionInput.jsx (Job input)
│   │   └── OptimizationResults.jsx (Results display)
│   └── hooks/
│       ├── useResumeOptimizer.js (Optimization logic)
│       └── useFileUpload.js (File handling)
└── ai/
    ├── prompts.py (AI prompt templates)
    └── keyword_matcher.py (Keyword extraction)
```

## 📝 Code Examples

### Backend Example: Resume Parsing

```python
# Parsing PDF resume
def parse_pdf(file):
    reader = PyPDF2.PdfReader(file)
    text = ""
    for page in reader.pages:
        text += page.extract_text()
    return text

# Parsing DOCX resume
def parse_docx(file):
    doc = Document(file)
    text = []
    for paragraph in doc.paragraphs:
        text.append(paragraph.text)
    return '\n'.join(text)
```

### Backend Example: AI Optimization

```python
# Using OpenAI to optimize resume
async def optimize_resume(resume_text, job_description):
    prompt = f"""
    Optimize this resume for the following job description:
    
    Job: {job_description}
    
    Resume: {resume_text}
    
    Return an optimized version that highlights relevant skills.
    """
    
    response = await openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    
    return response.choices[0].message.content
```

### Frontend Example: File Upload

```javascript
// Handling resume upload
const handleFileUpload = async (file) => {
  const formData = new FormData();
  formData.append('file', file);
  
  const response = await axios.post('/api/upload-resume', formData, {
    headers: { 'Content-Type': 'multipart/form-data' }
  });
  
  return response.data;
};
```

### Frontend Example: AI Suggestion Display

```javascript
// Displaying AI suggestions
const OptimizationResults = ({ suggestions }) => {
  return (
    <div className="results-container">
      {suggestions.map((suggestion, index) => (
        <div key={index} className="suggestion-card">
          <p className="original">{suggestion.original}</p>
          <p className="optimized">{suggestion.optimized}</p>
          <button onClick={() => acceptSuggestion(index)}>
            Accept
          </button>
        </div>
      ))}
    </div>
  );
};
```

## 🔒 Security Notes

- Validate file types before processing
- Check file sizes to prevent abuse
- Sanitize AI responses before displaying
- Use environment variables for API keys
- Implement rate limiting on API endpoints

## 🚀 Key Patterns

### API Pattern
```
Upload → Parse → Analyze → Optimize → Export
```

### AI Prompt Pattern
```
Context + Instructions + Data = Optimized Output
```

### Frontend Pattern
```
Upload → Preview → Optimize → Review → Export
```

## 💡 Tips

1. **PDF Parsing**: Some PDFs are images, not text - handle OCR if needed
2. **AI Prompts**: Iterate on prompts to get better results
3. **File Handling**: Validate files thoroughly before processing
4. **Error Handling**: Handle OpenAI API errors gracefully
5. **Formatting**: Preserve original formatting when possible

---

Add your code snippets here to help others learn!

