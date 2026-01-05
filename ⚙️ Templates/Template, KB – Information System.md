---
type: system
tags:
  - area/professional
  - system
last_reviewed: 2025-11-04
related: []
sources: []
poc:
ao:
so:
assessors:
aa:
atd:
---
# 📋 System Summary


---
# ⚙️ Components


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