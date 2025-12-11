# 🗓️ {{date:YYYY-MM-DD, dddd}}

## 🌤️ Focus & Priorities
Focus area of the day:
🔹 1. 
🔹 2. 
🔹 3. 

## 📋 Tasks


## 🧠 Notes & Ideas
- 

## 💭 Reflection (optional)
- 🌟 Highlight of the day:
- 💡 One insight or improvement:

## 🌱 Habit Tracker


> [!check] Quick End-of-Day Reflection  
> - 🌟 What went well today?  
> - ⚙️ What could go smoother tomorrow?  
> - 🙏 One small thing I’m grateful for.

---
# ❓ Questions
```dataviewjs
const tag = "#question"
const page = dv.current();
const lines = [];
 
for (let para of page.file.tasks || []) {
    if (para.text.includes(tag)) {
        lines.push(para.text);
    }
}
 
for (let para of page.file.lists || []) {
    if (para.text.includes(tag)) {
        lines.push(para.text);
    }
}
 
if (lines.length === 0) {
    dv.paragraph("No matching tags in this note.");
} else {
    dv.list(lines);
}
```