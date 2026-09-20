# MediAssist - Healthcare FAQ Conversational Agent

An evidence-based clinical triage, emergency red-flag screening, and OTC guidance AI assistant powered by FastAPI and Google Gemini AI.

---

## 📂 Project Architecture

The project is organized into clean, independent modules so that **Frontend** and **Backend** can be developed and deployed separately:

```
Healthcare-FAQ-Conversational-Agent/
│
├── backend/                  # FastAPI Python Service
│   ├── app.py                # REST API, Triage Engine & Gemini Integration
│   ├── requirements.txt      # Python dependencies
│   ├── Procfile              # Render / Railway process definition
│   ├── vercel.json           # Vercel serverless configuration
│   └── .env.example          # Backend environment variable template
│
├── frontend/                 # Static Responsive Web Application
│   ├── index.html            # User interface with markdown & triage badges
│   ├── config.js             # Configurable API base URL
│   ├── vercel.json           # Vercel static deployment configuration
│   └── .env.example          # Frontend environment template
│
├── docs/                     # Knowledge Base & Documentation
│   ├── DEPLOYMENT_GUIDE.md   # Step-by-step deployment instructions
│   ├── medical_faq.txt       # Clinical FAQ dataset
│   ├── medical_knowledge.txt # Evidence-based medical advice references
│   └── conversations.json    # Sample conversation history transcripts
│
├── .gitignore                # Strictly ignores all .env files, caches, and build artifacts
└── README.md                 # Project documentation
```

---

## 🚀 Quick Start (Local Development)

### 1. Start Backend

```bash
cd backend

# Create and activate virtual environment
python -m venv venv

# Windows:
venv\Scripts\activate
# macOS / Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Configure your Gemini API Key
cp .env.example .env
# Edit .env and set GOOGLE_API_KEY=your_key_here

# Run backend
uvicorn app:app --reload --port 8000
```
Backend will run at `http://localhost:8000`. You can test health at `http://localhost:8000/api/health` or view Swagger docs at `http://localhost:8000/docs`.

### 2. Start Frontend

Simply open `frontend/index.html` in any web browser, or serve it with:

```bash
cd frontend
python -m http.server 3000
```

Open `http://localhost:3000` in your browser.

> **Tip:** If your backend runs on a different port or domain, click **⚙️ API URL** in the header to set your custom backend URL (e.g., `http://localhost:8000` or `https://your-backend.onrender.com`).

---

## 🌐 Separate Deployment

For complete, step-by-step instructions on deploying the frontend to **Vercel** or **Netlify** and the backend to **Render**, **Railway**, or **Fly.io**, please read:

👉 **[docs/DEPLOYMENT_GUIDE.md](docs/DEPLOYMENT_GUIDE.md)**

---

## 🔒 Security & Environment Variables

- Never commit `.env` or `.env.*` files containing API keys to git.
- The root `.gitignore` is configured to prevent all `.env` files from being tracked.
- Use `.env.example` as a template for required variables.
