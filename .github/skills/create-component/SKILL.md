---
name: create-component
description: 'Create React components for Refuit project. Trigger: create component, new component, צור קומפוננטה, ליצור component, ליצור page, קומפוננטה חדשה'
argument-hint: 'Component name (PascalCase) and type'
---

# Create React Component

## When to Use
- Create reusable UI components
- Create full page screens with routing
- Generate forms, cards, or other React elements

## Process

1. **Ask**: Component name (PascalCase), type (component/page), complexity (simple/stateful/form/api)
2. **Location**: `client/src/components/` or `client/src/pages/`
3. **Generate** using template based on complexity
4. **If page**: Add route to `client/src/App.jsx`
5. **Output**: File location link + usage example

## Templates

**Simple**: Props only, no state  
**Stateful**: Includes `useState`  
**Form**: Full form with validation (9-digit ID, required fields)  
**API**: `useEffect` + fetch from backend

## Rules
- All comments in Hebrew (one line max)
- Always `dir="rtl"` on root element
- Use Tailwind CSS classes
- `export default` at end
- Props destructuring in function signature
- קוד תמציתי: אל תוסיף קוד מיותר, placeholder-ים ריקים, או תגובות ברורות מאליהן
- לא להוסיף prop-ים שלא נדרשו במפורש
- לא להוסיף פונקציות handler ריקות (e.g. `const handleX = () => {}`)
- לא להוסיף `console.log`, TODO comments, או קוד מוקמד (commented-out code)
- זה פרויקט לימודי: כתוב את המינימום הדרוש שעובד, לא production-grade boilerplate

## Example
```jsx
import { useState } from 'react';

// תיאור הקומפוננטה
function ComponentName({ prop1, onChange }) {
  const [value, setValue] = useState('');
  
  return (
    <div className="flex flex-col gap-4 p-4" dir="rtl">
      {/* תוכן */}
    </div>
  );
}

export default ComponentName;
```