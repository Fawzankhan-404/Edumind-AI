# EduMind AI

EduMind AI is a local-first student learning assistant rebuilt from the original EduMind AI project. The repository currently contains a React/Vite frontend and a Node.js/Express backend backed by MongoDB.

## Current features

- User registration and login with JWT authentication
- Student profile and progress flows
- PDF upload and document management
- Learning dashboard and course content
- AI chat, summaries, flashcards, and quizzes (optional; requires Gemini)
- Local development without a production API URL

## Requirements

Install these before starting:

- Node.js 20 or newer (includes npm)
- MongoDB 6+ running locally, or a reachable MongoDB connection string
- Git (optional, for cloning)
- A Gemini API key only if you want to use the AI-generation routes

The application is split into two processes. Start MongoDB first, then the backend, then the frontend.

## 1. Get the code

```bash
git clone https://github.com/Iqra403/Edumind-AI.git
cd Edumind-AI
```

If you are running the fork instead:

```bash
git clone https://github.com/Fawzankhan-404/Edumind-AI.git
cd Edumind-AI
```

## 2. Start MongoDB

Use a local MongoDB service, or provide a MongoDB URI in the backend environment file.

The default local database used below is:

```
mongodb://127.0.0.1:27017/edumind_ai
```

## 3. Configure and start the backend

From the repository root:

### macOS/Linux

```bash
cd Backend
npm install
cp .env.example .env
```

### Windows PowerShell

```powershell
cd Backend
npm install
Copy-Item .env.example .env
```

Open `Backend/.env` and set:

```env
PORT=8000
MONGODB_URI=mongodb://127.0.0.1:27017/edumind_ai
JWT_SECRET=replace-this-with-a-long-random-secret
JWT_EXPIRE=7d
FRONTEND_URL=http://localhost:5173
GEMINI_API_KEY=
```

Keep `GEMINI_API_KEY` empty for the core local app. Start the API:

```bash
npm run dev
```

The backend should be available at <http://localhost:8000/> and return `Backend is running`.

## 4. Configure and start the frontend

Open a second terminal at the repository root:

### macOS/Linux

```bash
cd Frontend
npm install
printf "VITE_API_URL=http://localhost:8000\\n" > .env
npm run dev
```

### Windows PowerShell

```powershell
cd Frontend
npm install
Set-Content .env "VITE_API_URL=http://localhost:8000"
npm run dev
```

Open the Vite URL shown in the terminal, normally <http://localhost:5173>. Restart the frontend after changing `Frontend/.env`.

## 5. Verify the local run

Check all three pieces:

1. MongoDB is running.
2. <http://localhost:8000/> shows `Backend is running`.
3. The frontend opens at <http://localhost:5173> and its network requests use `http://localhost:8000`.

Register a test account through the UI, sign in, and confirm that the dashboard loads.

## AI features

The application starts without a Gemini key. AI-generation endpoints intentionally return a clear `503` response until `GEMINI_API_KEY` is configured.

To enable them:

1. Add your key to `Backend/.env`.
2. Stop and restart the backend.
3. Use the AI features from the frontend.

Never commit `Backend/.env`, API keys, JWT secrets, or uploaded documents.

## Useful checks

Frontend checks run from `Frontend`:

```bash
npm run lint
npm run build
```

The backend currently has no separate lint or test script. At minimum, verify that `npm run dev` starts and that the root endpoint responds.

## Troubleshooting

- **MongoDB connection error:** confirm MongoDB is running and that `MONGODB_URI` points to the correct host and database.
- **Port 8000 already in use:** change `PORT` in `Backend/.env`, then set the matching `VITE_API_URL`.
- **CORS error:** make sure `FRONTEND_URL` exactly matches the frontend origin, including the port.
- **AI disabled:** this is expected when `GEMINI_API_KEY` is empty; configure the key only when AI features are needed.
- **Frontend still calls an old API:** confirm `Frontend/.env` contains `VITE_API_URL=http://localhost:8000` and restart Vite.

## Project scope

The current implementation is the Node.js/Express/MongoDB application described above. Java/Spring Boot, MySQL, Groq, exam-readiness, and smart-planner items from the original concept README are roadmap ideas, not completed features in this repository.

## Source and contribution

The project was rebuilt from `Nikita-Bhange/EduMind_Ai` for development in `Iqra403/Edumind-AI`. Please open an issue or pull request with reproducible steps when improving the local setup or application.
