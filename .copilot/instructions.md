# Refuit - Development Guidelines

## Tech Stack
- **Frontend:** React + Vite, React Router, Tailwind CSS
- **Backend:** Node.js + Express (REST API)
- **DB:** MongoDB with Mongoose (local connection: `mongodb://localhost:27017/refuit`)

## Project Structure
- `/client/src/pages/` - Screens: Login, Register, PatientList, PatientRecord
- `/client/src/components/` - Shared components
- `/server/models/` - Mongoose models: Doctor, Patient, Appointment, Visit, TestResult, Medication
- `/server/routes/` - auth, patients, visits, tests, medications, appointments

## Rules
- Full RTL interface in Hebrew
- Auth: compare username & password against MongoDB, store session in localStorage
- Every protected route checks `localStorage` before accessing data
- Summary letter: use `mailto:` only — opens the user's local mail client (Outlook/Gmail) with recipient and content pre-filled; the user clicks Send manually. No server or API involved.
- Passwords stored as plain text (academic project)
- Required fields: ID number (9 digits), full name, date

## Code Comments
- All inline code comments must be in Hebrew only, concise (one line max)