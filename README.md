# AI PPT Generator

An AI-powered web application that generates PowerPoint presentations from a topic or description using Claude (Anthropic LLM) + FastAPI + python-pptx.

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Python, FastAPI |
| LLM | Anthropic Claude (claude-sonnet) |
| PPT Generation | python-pptx |
| Frontend | HTML, CSS, JavaScript |
| Server | Uvicorn (ASGI) |

---

## Setup Instructions

### 1. Clone / download the project

```
ppt_generator/
├── main.py
├── requirements.txt
├── static/
│   └── index.html
└── README.md
```

### 2. Create a virtual environment

```bash
python -m venv venv
source venv/bin/activate        # Linux / Mac
venv\Scripts\activate           # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set your Anthropic API key

```bash
# Linux / Mac
export ANTHROPIC_API_KEY=your_api_key_here

# Windows (Command Prompt)
set ANTHROPIC_API_KEY=your_api_key_here

# Windows (PowerShell)
$env:ANTHROPIC_API_KEY="your_api_key_here"
```

Get your API key from: https://console.anthropic.com

### 5. Run the server

```bash
cd ppt_generator
uvicorn main:app --reload
```

### 6. Open in browser

```
http://localhost:8000
```

---

## Features

- Enter any topic or description
- Choose number of slides (5, 7, or 10)
- Choose a theme (Professional / Minimal / Vibrant)
- Claude generates structured slide content (titles + bullet points)
- python-pptx builds a properly formatted .pptx file
- Download button appears instantly after generation

---

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | Serves the web UI |
| POST | `/generate` | Generates the presentation |
| GET | `/download/{filename}` | Downloads the .pptx file |

### POST /generate — Request body

```json
{
  "topic": "Introduction to Machine Learning",
  "description": "For college students, focus on basics",
  "slide_count": 7,
  "theme": "professional"
}
```

### POST /generate — Response

```json
{
  "filename": "abc123.pptx",
  "slides": [
    { "slide": 1, "title": "Introduction to Machine Learning", "bullets": ["..."] },
    ...
  ],
  "download_url": "/download/abc123.pptx"
}
```

---

## Notes

- Generated .pptx files are stored in `/tmp/` and are temporary
- Minimum 5 slides, maximum 15 slides per presentation
- Requires an active internet connection (for Anthropic API calls)
