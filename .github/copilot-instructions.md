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

## Skill Structure

When creating a new skill, you MUST follow this exact process — no exceptions:

1. Use the `read_file` tool to load the skill file listed below.
2. Read the ENTIRE file before doing anything else.
3. Follow EVERY step in the file exactly, in order.
4. Do NOT skip any step, including registering the skill in this file.

If you cannot read the skill file, stop and tell the user — do not proceed from memory.

---

### Registered Skills

- **microsoft-skill-creator** – Generates a new skill. Trigger words: "create skill", "generate skill", "צור סקיל", "ליצירת סקיל".  
  ⚠️ MANDATORY: Before doing ANYTHING else, call `read_file` on `.github/skills/microsoft-skill-creator/skills.md` and follow all steps inside it without exception.

- **create-component** – Creates new React components for Refuit project. Trigger words: "create component", "new component", "צור קומפוננטה", "ליצור component", "ליצור page", "קומפוננטה חדשה".  
  ⚠️ MANDATORY: Before doing ANYTHING else, call `read_file` on `.github/skills/create-component/SKILL.md` and follow all steps inside it without exception.

---

### How to Register a New Skill (after completing it)

After finishing a skill, add an entry here in this format:

- **skill-name** – One-line description. Trigger words: "...".  
  ⚠️ MANDATORY: Before doing ANYTHING else, call `read_file` on `.github/skills/skill-name/SKILL.md` and follow all steps inside it without exception.

