# CounterDiab

A from-scratch, responsive full-stack educational demo for exploring diabetes risk factors. This is not a replica of the missing `CounterDiab Demo.html`; it uses an original visual design because the source file was not provided.

## What is included

- `frontend/`: Next.js, React and TypeScript single-page experience with Home, About, Prediction, Assessment Results and Model Dashboard sections.
- `backend/`: FastAPI endpoints for health, assessment/prediction and model status.
- `render.yaml`: Render service definition for the API.
- No database: assessments are processed in memory and are not retained.

## Important model status

There was no source HTML, trained model, training dataset, or clinical validation artifact in the supplied files. The API therefore uses an explicitly disclosed illustrative rules-based score. Its values are not learned, calibrated, validated, or suitable for diagnosis or treatment. Dashboard model metrics are intentionally unavailable. Replace the demo assessment implementation only when a documented, validated model is provided.

## Run locally

Backend (Python 3.10+):

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
$env:CORS_ORIGINS='http://localhost:3000'
uvicorn main:app --reload --port 8000
```

Frontend (Node.js):

```powershell
cd frontend
Copy-Item .env.example .env.local
npm install
npm run dev
```

Open `http://localhost:3000`. The frontend calls `http://localhost:8000` by default. Set `NEXT_PUBLIC_API_URL` to the deployed API origin for production.

## Deploy

### Render API

Connect this repository to Render and use the root `render.yaml` Blueprint. It installs `backend/requirements.txt`, runs `uvicorn main:app --host 0.0.0.0 --port $PORT`, and checks `/health`. After the API is created, set `CORS_ORIGINS` to the exact Vercel production origin (for example `https://your-project.vercel.app`).

### Vercel frontend

Import this repository into Vercel and set the project Root Directory to `frontend`. Add `NEXT_PUBLIC_API_URL` with the Render API origin (for example `https://counterdiab-api.onrender.com`), then deploy.

PostgreSQL is not configured because no persistence is needed for session-only demo assessments. No results endpoint is offered because results are not stored.
