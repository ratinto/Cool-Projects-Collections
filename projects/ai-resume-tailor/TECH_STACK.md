# 🛠️ Tech Stack Details

Here's everything I used to build this. Some choices worked out well, others... not so much.

## Frontend Technologies

### React.js
- **Version**: 18.2.0+
- **Why**: Most familiar framework, huge ecosystem
- **Key Features**: Component-based, hooks, good docs
- **Use Cases**: UI, file upload, document preview

### Tailwind CSS
- **Version**: 3.3+
- **Why**: Fast styling, don't want to write custom CSS
- **Key Features**: Utility classes, responsive design
- **Use Cases**: Layout, components, responsive design

### Headless UI
- **Version**: Latest
- **Why**: Accessible components, good styling hooks
- **Key Features**: Unstyled components, accessibility built-in
- **Use Cases**: Dropdowns, modals, UI elements

### Zustand
- **Version**: Latest
- **Why**: Lightweight state management, simpler than Redux
- **Key Features**: Easy to use, no boilerplate
- **Use Cases**: File state, resume data, UI state

### react-pdf
- **Version**: Latest
- **Why**: Need to preview PDFs in the browser
- **Key Features**: PDF rendering, page navigation
- **Use Cases**: Resume preview, document viewing

### react-dropzone
- **Version**: Latest
- **Why**: Easy file upload with drag-and-drop
- **Key Features**: File validation, drag drop support
- **Use Cases**: Resume upload, job description upload

## Backend Technologies

### Python
- **Version**: 3.10+
- **Why**: Better NLP libraries than Node.js
- **Key Features**: Great for text processing
- **Use Cases**: Document parsing, AI integration

### Flask/FastAPI
- **Version**: Latest
- **Why**: FastAPI is fast and has good async support
- **Key Features**: Auto API docs, easy to use
- **Use Cases**: API endpoints, file handling

### OpenAI API
- **Why**: Best AI models for text generation
- **Key Features**: GPT models, prompt-based
- **Use Cases**: Resume rewriting, keyword matching

**Warning:** API costs can add up quickly during testing!

### PyPDF2
- **Version**: Latest
- **Why**: Parse PDF files
- **Key Features**: Text extraction, page handling
- **Use Cases**: PDF parsing, text extraction

### python-docx
- **Version**: Latest
- **Why**: Handle Word documents
- **Key Features**: Read/write Word docs, formatting
- **Use Cases**: DOCX parsing, document generation

### spaCy
- **Version**: Latest
- **Why**: NLP library for text analysis
- **Key Features**: Tokenization, entity recognition
- **Use Cases**: Keyword extraction, text analysis

### pdfkit
- **Version**: Latest
- **Why**: Generate PDFs from HTML
- **Key Features**: HTML to PDF conversion
- **Use Cases**: Resume PDF generation

## DevOps & Tools

### Docker
- **Version**: Latest
- **Why**: Consistent environments
- **Key Features**: Containerization
- **Use Cases**: Development, deployment

### Vercel
- **Why**: Easy React deployment
- **Key Features**: Auto deployments, edge network
- **Use Cases**: Frontend hosting

### Railway/Render
- **Why**: Simple Python hosting
- **Key Features**: Easy deployment, automatic HTTPS
- **Use Cases**: Backend hosting

### Jest
- **Version**: Latest
- **Why**: Testing framework
- **Key Features**: Unit tests, integration tests
- **Use Cases**: Frontend testing

### Pytest
- **Version**: Latest
- **Why**: Python testing framework
- **Key Features**: Easy to use, good fixtures
- **Use Cases**: Backend testing

## Required Python Packages

```txt
fastapi==0.104.1
uvicorn==0.24.0
openai==1.3.0
PyPDF2==3.0.1
python-docx==1.1.0
spacy==3.7.2
python-multipart==0.0.6
pydantic==2.5.0
pdfkit==1.0.0
pytest==7.4.3
```

## Required Node.js Packages

```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "zustand": "^4.4.6",
    "react-pdf": "^7.5.3",
    "react-dropzone": "^14.2.3",
    "axios": "^1.6.0",
    "@headlessui/react": "^1.7.17",
    "tailwindcss": "^3.3.5"
  },
  "devDependencies": {
    "vite": "^5.0.0",
    "@vitejs/plugin-react": "^4.2.0",
    "eslint": "^8.53.0",
    "prettier": "^3.0.3"
  }
}
```

## Architecture Decisions

### Why Flask/FastAPI?
FastAPI has better async support and auto-generates API docs. Makes testing easier.

### Why Python for Backend?
Python has way better NLP libraries than Node.js. spaCy and NLTK are solid choices.

### Why Zustand over Redux?
Zustand is way simpler and has less boilerplate. Don't need all of Redux's complexity for this.

### Why react-pdf?
Need to preview PDFs in browser before processing. react-pdf handles this well.

### PDF Generation Challenges
PDF generation is honestly the hardest part. Tried several libraries before settling on pdfkit. Even then, formatting can be tricky.

---

That's the tech stack! Pretty standard choices for a Python + React app.

