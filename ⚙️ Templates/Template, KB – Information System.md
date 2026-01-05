---
type: system
tags:
  - area/professional
  - system
last_reviewed: 2025-11-04
related: []
ao:
so:
assessors:
aa:
atd:
pii:
impact_level:
---
# 📋 System Summary
**[Archer Link]()**

| System Property                | Status                |
| ------------------------------ | --------------------- |
| Impact Level                   | `= this.impact_level` |
| Authorizing Official           | `= this.ao`           |
| System Owner                   | `= this.so`           |
| Assessors                      | `= this.assessors`    |
| Authorization Termination Date | `= this.atd`          |
| Annual Assessment Due          | `= this.aa`           |
| Contains PII                   | `= this.pii`          |
## Description


---
# ⚙️ Components


---
# 📝 Notes


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