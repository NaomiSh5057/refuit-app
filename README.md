# Refuit — Medical Documentation App
A lightweight web app for recording patient visits, test results, medications, and summary letters.

Key features:
- Patient visit notes, history, test results, medications.
- Appointment management and summary letter generation (mailto/print).

Tech stack:
- Frontend: React + Vite, Tailwind/MUI; Backend: Node.js + Express; DB: MongoDB + Mongoose.

Quick start:
1. Install dependencies in client/ and server/ with `npm install`.
2. Start MongoDB locally and set `.env` `MONGODB_URI`.
3. Run server: `node server/index.js` and client: `npm run dev` in `client/`.

Env:
- PORT=5000
- MONGODB_URI=mongodb://localhost:27017/refuit

Educational demo: passwords stored in plain text for learning purposes.
