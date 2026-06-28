# Refuit — מערכת לתיעוד רפואי
### מסמך אפיון מערכת | גרסה 1.0 | יוני 2026 | נוצר ע"י נעמי שניידר

---

## 1. סקירה כללית

מערכת Refuit היא אפליקציית Web לתיעוד רפואי, המיועדת לניהול ביקורי מטופלים, שמירת היסטוריה רפואית, תוצאות בדיקות ותרופות קבועות, ולהנפקת מכתבי סיכום רפואיים. המערכת מתוכננת להיות קטנה ויעילה, מתאימה לפרויקט לימודי עם מינימום שתי שעות עבודה בסביבת AI Agents.

### 1.1 מטרות המערכת
- מתן ממשק מרכזי לרופאים לתיעוד ביקורים רפואיים
- שמירת היסטוריה רפואית מלאה לכל מטופל
- ניהול תרופות קבועות ותוצאות בדיקות
- הנפקה ושיתוף מכתבי סיכום רפואיים
- ניהול תורים על ידי מזכירה

### 1.2 משתמשי המערכת

| משתמש | תפקיד |
|--------|--------|
| רופא | כניסה למערכת, צפייה ברשימת המטופלים שלו, תיעוד ביקורים, עדכון מידע רפואי, הנפקת מכתבי סיכום |
| מזכירה | קביעת תורים, הזנת מטופלים חדשים לרשימה |
| מנהל מערכת | הרשמת רופאים חדשים (בשלב הראשוני ייתכן שזהה לרופא הראשי) |

---

## 2. ארכיטקטורה וטכנולוגיות

### 2.1 סקירת ארכיטקטורה

| שכבה | טכנולוגיה | תפקיד |
|------|-----------|--------|
| Frontend | React + Vite | ממשק המשתמש — SPA מהיר ומודרני |
| ניתוב | React Router | ניהול ניווט בין מסכים |
| עיצוב | Tailwind CSS / MUI | סטיילינג מהיר ועקבי |
| Backend | Node.js + Express | API Server — REST API |
| אימות | localStorage Session | שמירת פרטי הרופא המחובר בצד הלקוח |
| מסד נתונים | MongoDB Community | שמירת כל הנתונים — גרסה מקומית חינמית |
| ORM | Mongoose | מודלים ו-schema validation |
| מייל | mailto: link | פתיחת לקוח המייל של המשתמש לשליחת מכתב |

### 2.2 מבנה פרויקט

```
refuit/
├── client/                  # React + Vite Frontend
│   ├── src/
│   │   ├── pages/
│   │   │   ├── Login.jsx
│   │   │   ├── Register.jsx
│   │   │   ├── PatientList.jsx
│   │   │   └── PatientRecord.jsx
│   │   ├── components/
│   │   │   ├── Tabs/
│   │   │   └── SummaryLetter.jsx
│   │   ├── api/
│   │   └── App.jsx
│   └── vite.config.js
└── server/                  # Node.js + Express Backend
    ├── models/
    │   ├── Doctor.js
    │   ├── Patient.js
    │   ├── Appointment.js
    │   ├── Visit.js
    │   ├── TestResult.js
    │   └── Medication.js
    ├── routes/
    │   ├── auth.js
    │   ├── patients.js
    │   ├── visits.js
    │   ├── tests.js
    │   ├── medications.js
    │   └── appointments.js
    └── index.js
```

---

## 3. מודל נתונים (MongoDB)

### Doctors — רופאים
| שדה | סוג | תיאור |
|-----|-----|--------|
| _id | ObjectId | אוטומטי |
| username | String | שם משתמש (ייחודי) |
| password | String | סיסמא (טקסט פשוט, לצרכי לימוד) |
| fullName | String | שם מלא |
| specialty | String | תחום התמחות |
| email | String | כתובת מייל |
| createdAt | Date | תאריך יצירה |

### Patients — מטופלים
| שדה | סוג | תיאור |
|-----|-----|--------|
| _id | ObjectId | אוטומטי |
| idNumber | String | תעודת זהות (ייחודי) |
| fullName | String | שם מלא |
| dateOfBirth | Date | תאריך לידה |
| phone | String | טלפון |
| email | String | אימייל |
| createdAt | Date | תאריך יצירה |

### Appointments — תורים
| שדה | סוג | תיאור |
|-----|-----|--------|
| _id | ObjectId | אוטומטי |
| patientId | ObjectId | ref: Patient |
| doctorId | ObjectId | ref: Doctor |
| date | Date | תאריך הביקור |
| time | String | שעת הביקור (HH:MM) |
| status | String | pending / completed / cancelled |

### Visits — ביקורים (תיעוד רפואי)
| שדה | סוג | תיאור |
|-----|-----|--------|
| _id | ObjectId | אוטומטי |
| patientId | ObjectId | ref: Patient |
| doctorId | ObjectId | ref: Doctor |
| appointmentId | ObjectId | ref: Appointment (אופציונלי) |
| visitDate | Date | תאריך הביקור |
| chiefComplaint | String | תלונה עיקרית |
| anamnesis | String | אנמנזה |
| physicalExam | String | ממצאי בדיקה גופנית |
| diagnosis | String | אבחנה |
| treatment | String | טיפול מומלץ |
| notes | String | הערות נוספות |
| createdAt | Date | תאריך יצירה |

### TestResults — תוצאות בדיקות
| שדה | סוג | תיאור |
|-----|-----|--------|
| _id | ObjectId | אוטומטי |
| patientId | ObjectId | ref: Patient |
| doctorId | ObjectId | ref: Doctor |
| testName | String | שם הבדיקה |
| testDate | Date | תאריך הבדיקה |
| result | String | תוצאה |
| normalRange | String | טווח נורמה (אופציונלי) |
| notes | String | הערות |
| createdAt | Date | תאריך יצירה |

### Medications — תרופות קבועות
| שדה | סוג | תיאור |
|-----|-----|--------|
| _id | ObjectId | אוטומטי |
| patientId | ObjectId | ref: Patient |
| doctorId | ObjectId | אחראי הרישום |
| medicationName | String | שם התרופה |
| dosage | String | מינון (למשל: 10mg) |
| frequency | String | תדירות (למשל: פעם ביום) |
| startDate | Date | תאריך התחלה |
| notes | String | הערות |
| isActive | Boolean | האם פעיל |

---

## 4. תיאור מסכים

### 4.1 מסך התחברות / הרשמה
**כתובת:** `/login` | `/register`

מסך ראשון שמוצג לרופא. קיימות שתי אפשרויות: כניסה עם שם משתמש וסיסמא קיימים, או הרשמה ראשונית.

**שדות הרשמה:** שם מלא, שם משתמש, סיסמא (+ אישור), תחום התמחות, אימייל

**שדות כניסה:** שם משתמש, סיסמא

**לוגיקת Backend:**
- `POST /api/auth/register` — יצירת רופא חדש, שמירת פרטים ב-MongoDB
- `POST /api/auth/login` — בדיקת שם משתמש וסיסמא, החזרת פרטי הרופא
- פרטי הרופא המחובר נשמרים ב-`localStorage`

---

### 4.2 מסך רשימת מטופלים
**כתובת:** `/patients`

לאחר כניסה מוצלחת — רשימת המטופלים הממתינים לרופא.

| שם המטופל | תעודת זהות | תאריך ביקור | שעה | תחום הרופא |
|-----------|-----------|------------|-----|------------|
| ישראל ישראלי | 123456789 | 15/06/2025 | 10:30 | קרדיולוגיה |
| שרה כהן | 987654321 | 15/06/2025 | 11:00 | קרדיולוגיה |

**פעולות:** לחיצה על שורה → מסך הרופא | כפתור "קביעת תור" | סינון לפי תאריך

---

### 4.3 מסך קביעת תורים
**כתובת:** `/appointments/new`

**שדות:** שם מטופל / חיפוש לפי ת.ז., תאריך, שעה, בחירת רופא, הערות

---

### 4.4 מסך הרופא (Patient Record)
**כתובת:** `/patients/:patientId`

כותרת: שם המטופל + ת.ז. + חץ חזרה לרשימה

#### לשונית 1: ביקור רופא
| שדה | תיאור |
|-----|--------|
| תאריך ביקור | אוטומטי, ניתן לשינוי |
| תלונה עיקרית | שדה טקסט |
| אנמנזה | textarea |
| בדיקה גופנית | textarea |
| אבחנה | שדה טקסט |
| טיפול מומלץ | textarea |
| הערות נוספות | textarea |

כפתורים: `[שמור ביקור]` `[נקה שדות]`

#### לשונית 2: ביקורים קודמים
היסטוריה מלאה — קארדים מקופלים ממוינים מהחדש לישן.  
כל קארד: תאריך, שם רופא, תלונה עיקרית, אבחנה + כפתור "הצג פרטים מלאים"

#### לשונית 3: תוצאות בדיקות
טבלה: שם בדיקה | תאריך | תוצאה | טווח נורמה | הערות  
כפתור "הוסף בדיקה" → פורם עם שדות + `[שמור]` `[בטל]`

#### לשונית 4: תרופות קבועות
טבלה: שם תרופה | מינון | תדירות | תאריך התחלה | הערות | סטטוס  
כפתור "הוסף תרופה" → פורם עם שדות + `[שמור]` `[בטל]`

---

### 4.5 מכתב סיכום
כפתור "מכתב סיכום" — זמין בכל לשונית.

**תוכן המכתב:**
- פרטי מטופל (שם, ת.ז., תאריך לידה)
- פרטי הרופא המוציא
- תאריך הפקה
- סיכום ביקור נוכחי
- סיכום ביקורים קודמים
- תוצאות בדיקות אחרונות
- רשימת תרופות קבועות פעילות

**פעולות:**
- `[שלח במייל]` — פותח `mailto:` עם תוכן ממולא, המשתמש שולח בעצמו
- `[הדפסה]` — `window.print()` עם CSS מותאם
- תצוגה מקדימה לפני שליחה/הדפסה

---

## 5. API Endpoints

| Method | Endpoint | Auth | תיאור |
|--------|----------|------|--------|
| POST | /api/auth/register | ללא | הרשמת רופא חדש |
| POST | /api/auth/login | ללא | כניסה למערכת |
| GET | /api/patients | Session | רשימת מטופלים + תורים |
| GET | /api/patients/:id | Session | פרטי מטופל |
| POST | /api/patients | Session | הוספת מטופל חדש |
| GET | /api/visits/:patientId | Session | ביקורים קודמים |
| POST | /api/visits | Session | שמירת ביקור חדש |
| GET | /api/tests/:patientId | Session | תוצאות בדיקות |
| POST | /api/tests | Session | הוספת תוצאת בדיקה |
| GET | /api/medications/:patientId | Session | תרופות קבועות |
| POST | /api/medications | Session | הוספת תרופה |
| PUT | /api/medications/:id | Session | עדכון תרופה |
| GET | /api/summary/:patientId | Session | נתונים למכתב סיכום |
| POST | /api/appointments | Session | קביעת תור חדש |

---

## 6. תוכנית עבודה — שתי שעות עם AI Agents

| זמן | שלב | משימות |
|-----|-----|--------|
| 0:00–0:20 | הקמה | יצירת מבנה Vite + React, התקנת MongoDB Community מקומי, npm install |
| 0:20–0:40 | Backend | מודלי Mongoose, Express server, auth routes (register/login + session) |
| 0:40–1:00 | Frontend Auth | מסכי Login + Register, חיבור ל-API, ניהול localStorage |
| 1:00–1:20 | רשימת מטופלים | מסך Patient List, API GET /patients, תצוגת תורים |
| 1:20–1:40 | מסך הרופא | 4 לשוניות — ביקור רופא, ביקורים קודמים, בדיקות, תרופות |
| 1:40–2:00 | סיום | מכתב סיכום, כפתורי mailto/הדפסה, בדיקות סיום |

---

## 7. אבטחה ושיקולים נוספים

### 7.1 אימות גישה
- סיסמאות נשמרות כטקסט פשוט (plain text) — מתאים לפרויקט לימודי
- Session פשוט ב-`localStorage` לשמירת פרטי הרופא המחובר
- בדיקת התחברות: השוואת שם משתמש וסיסמא מול MongoDB
- הפרדת נתונים: רופא רואה רק את המטופלים שלו

### 7.2 ולידציות
- ת.ז. — 9 ספרות, ולידציה בצד הלקוח והשרת
- שדות חובה מסומנים ומוגנים
- Sanitization של קלטי משתמש

### 7.3 UI/UX
- ממשק RTL מלא בעברית
- תצוגה רספונסיבית (Desktop בעיקר)
- Loading states בזמן קריאות API
- הודעות שגיאה ברורות למשתמש

---

## 8. משתני סביבה (.env)

```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/refuit
```

---

*מסמך אפיון — Refuit | גרסה 1.0*