# SkillBridge

Career platform that tells students how well their skills match a job, what's missing, and how to close the gap.

**Stack:** React (Vite) · Node.js + Express · MongoDB (Mongoose) · JWT

## Flow
Login/Register → Student profile → Add skills → Job portal → ⭐ Match score → ⭐ Skill gap → ⭐ Roadmap → Application tracking

## Run it

### 1. Backend
```bash
cd server
cp .env.example .env      # edit MONGO_URI / JWT_SECRET
npm install
npm run seed              # optional demo data
npm run dev               # http://localhost:5000
```

### 2. Frontend
```bash
cd client
npm install
npm run dev               # http://localhost:5173  (proxies /api to :5000)
```

Demo logins after seeding (password `demo123`): `student@demo.com`, `recruiter@demo.com`

## How the match score works (`server/utils/match.js`)
score = Σ weight(skill level) / number of required skills × 100
Weights: advanced 1.0, intermediate 0.8, beginner 0.5. Missing skills = the skill gap; each one becomes a roadmap step (`server/utils/roadmap.js`).

## API
| Method | Route | Role |
|---|---|---|
| POST | /api/auth/register, /login | all |
| GET | /api/auth/me | all |
| PUT | /api/profile | student |
| POST/DELETE | /api/profile/skills | student |
| POST | /api/profile/resume | student |
| GET | /api/jobs?q=&type= | student (with match scores) |
| GET | /api/jobs/:id | student (match + gap + roadmap) |
| POST | /api/jobs | recruiter |
| GET | /api/jobs/mine/list | recruiter |
| GET | /api/jobs/:id/candidates | recruiter (ranked) |
| POST | /api/applications/:jobId | student |
| GET | /api/applications/mine | student |
| PATCH | /api/applications/:id/status | recruiter |
