# Deployment Guide: Healthcare FAQ Conversational Agent

This guide walks you through deploying the **Frontend** and **Backend** as separate, independent services.

---

## 🏗️ Architecture Overview

```
Healthcare-FAQ-Conversational-Agent/
├── backend/          # FastAPI REST API (Symptom analysis, Gemini AI, Red-flag screening)
├── frontend/         # Pure Web UI (HTML5, Vanilla CSS, Responsive, Markdown rendering)
└── docs/             # Clinical FAQs, knowledge bases, and documentation
```

- **Frontend** can be hosted on **Vercel**, **Netlify**, **Cloudflare Pages**, or **GitHub Pages**.
- **Backend** can be hosted on **Render**, **Railway**, **Fly.io**, **Google Cloud Run**, or **Vercel Serverless**.

---

## 🚀 Option 1: Deploy Backend to Render (Recommended for Python)

[Render](https://render.com) offers simple hosting for Python Web Services.

### Steps:
1. Create a free account at [render.com](https://render.com).
2. Click **New +** -> **Web Service**.
3. Connect your GitHub repository.
4. Configure the service:
   - **Name:** `mediassist-backend` (or your choice)
   - **Root Directory:** `backend`
   - **Environment:** `Python 3`
   - **Build Command:** `pip install -r requirements.txt`
   - **Start Command:** `uvicorn app:app --host 0.0.0.0 --port $PORT`
5. Under **Environment Variables**, add:
   - `GOOGLE_API_KEY`: Your Gemini API key from [Google AI Studio](https://aistudio.google.com/).
6. Click **Deploy Web Service**.
7. Once deployed, copy your backend URL (e.g., `https://mediassist-backend.onrender.com`).

---

## 🌐 Option 2: Deploy Frontend to Vercel

### Steps:
1. Go to [vercel.com](https://vercel.com) and log in.
2. Click **Add New...** -> **Project**.
3. Import your GitHub repository.
4. In the project setup screen:
   - **Root Directory:** Click "Edit" and select `frontend`.
   - **Framework Preset:** `Other`.
5. Click **Deploy**.
6. After deployment, open your frontend site (e.g. `https://your-project.vercel.app`).

### Linking Frontend to Backend:
There are two ways to connect your deployed frontend to your deployed backend:

- **Method A (No code change):** Click the **⚙️ Settings** icon in the top header of the web page, paste your backend URL (e.g. `https://mediassist-backend.onrender.com`), and click **Save**. It will be preserved in your browser!
- **Method B (Permanent config):** In `frontend/config.js`, set:
  ```javascript
  window.API_BASE_URL = "https://mediassist-backend.onrender.com";
  ```
  Commit and push to GitHub.

---

## ⚡ Option 3: Deploy Backend as Serverless Function on Vercel

If you prefer to keep both frontend and backend on Vercel:

1. Import the repository into Vercel twice:
   - **Project 1 (Frontend):** Root directory `frontend`.
   - **Project 2 (Backend):** Root directory `backend`.
2. In Project 2 (Backend), add the environment variable:
   - `GOOGLE_API_KEY`: Your Gemini API key.
3. Use the generated Backend URL in the Frontend.

---

## 💻 Local Development

### 1. Run Backend
```bash
cd backend
python -m venv venv
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

pip install -r requirements.txt
cp .env.example .env
# Edit .env and add your GOOGLE_API_KEY

uvicorn app:app --reload --port 8000
```
Backend will run at `http://localhost:8000`.

### 2. Run Frontend
Open `frontend/index.html` in your browser (or use VS Code "Live Server", or `python -m http.server 3000` inside `frontend/`).
Ensure the backend URL is set to `http://localhost:8000` in the UI settings or `config.js`.
