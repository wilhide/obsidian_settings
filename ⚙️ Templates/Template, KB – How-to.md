---
type: howto
tags:
  - knowledge
  - area/professional
title:
summary:
last_reviewed: 2025-11-04
related: []
sources: []
poc:
---
> [!check] **How-to or something else?**
> Use this note for **step-by-step procedures** you might repeat or teach.  
> It focuses on *doing*, not just *understanding*.  
> If you’re explaining **why** something works, use a 🧩 *Concept*.  
> If you’re documenting a **multi-phase scenario**, use a 🎛️ *Playbook*.  
> If you’re formalizing a **design or structure**, use a 🧱 *Pattern*.  
> If you’re compiling **experiments or findings**, use a 🔬 *Research* note.

---
> [!info] **TL;DR**
> Describe what this How-to accomplishes and when to use it (1–3 sentences).

---
# ⚙️ Prerequisites
> [!tip]
> List what must be true or available before starting — tools, permissions, context, or files.

- 
- 

---
# 🚀 Steps
> [!tip]
> Write the ordered sequence needed to complete the task.  
> Include code blocks, commands, or screenshots if relevant.

1. 
2. 
3. 

---
# ✅ Verification
> [!tip]
> Explain how to confirm the task succeeded — logs, output, behavior, or visual cues.

- 

---
# 🧯 Troubleshooting
> [!tip]
> Capture known issues, error messages, and their solutions.  
> This section becomes invaluable when something breaks later.

- 

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