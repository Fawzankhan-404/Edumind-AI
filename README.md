# EduMind AI

EduMind AI is a local-first student learning assistant rebuilt from the original EduMind AI project.

## What is included

- React/Vite frontend
- Node.js/Express backend
- MongoDB/Mongoose persistence
- JWT authentication
- PDF upload and document management
- AI chat, summaries, flashcards, and quizzes
- Progress dashboard and profile flows

## Run locally

### Requirements

- Node.js 20+
- MongoDB running locally, or an approved MongoDB connection string
- A Gemini API key only for the AI-generation routes

### Backend

```bash
cd Backend
npm install
copy .env.example .env
npm run dev
```

The API runs on `http://localhost:8000`.

### Frontend

```bash
cd Frontend
npm install
npm run dev
```

The frontend uses `http://localhost:8000` by default. To change it, create `Frontend/.env` with:

```
VITE_API_URL=http://localhost:8000
```

## Environment

Copy `Backend/.env.example` to `Backend/.env`. Never commit real credentials.

- `MONGODB_URI` and `JWT_SECRET` are required.
- `GEMINI_API_KEY` is required only for AI generation features.
- `FRONTEND_URL` should match the local frontend origin.

## Current scope

The current codebase is a Node/Express/MongoDB implementation. The Java/Spring Boot, MySQL, Groq, exam-readiness meter, and smart-planner items from the original concept README remain future roadmap work and are not presented as completed features.

## Source

The application source originated from `Nikita-Bhange/EduMind_Ai` and is being rebuilt in `Iqra403/Edumind-AI`.
