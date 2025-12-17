---
type: meeting
tags:
  - area/professional
  - reference
  - meeting
date: <% tp.date.now("YYYY-MM-DD") %>
attendees: []
project: 
related: []
---
> [!summary] Purpose
> Briefly state the objective of this meeting.
- 

---
# 📝 Agenda
- 

---
# 🗒️ Notes
- <% tp.file.cursor(1) %>

---
# 🔃 Follow-ups & Tasks

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