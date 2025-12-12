---
type: concept
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
> [!check] **Concept or something else?**
> Use this note for *understanding*, not *doing*.  
> It explains **what something is**, **why it matters**, and **how it connects** to other ideas.  
> If you’re documenting **steps**, use a 🛠️ *How-to*.  
> If you’re handling a **recurring scenario**, use a 🎛️ *Playbook*.  
> If you’re capturing a **design approach**, use a 🧱 *Pattern*.  
> If you’re gathering **research or source material**, use a 🔬 *Research* note.

---
> [!info] **TL;DR**
> Summarize this concept in 2–4 sentences. What is it, why does it matter, and when would you apply it?

---
# 💡 Key Principles
> [!tip]
> Capture the core truths or rules that define this concept. These are the takeaways you’d want to remember without rereading the full note.

- 
- 
- 

---
# 🧠 Example / Application
> [!tip]
> Ground the idea with a real or imagined scenario, analogy, or command sequence.  
> Ask yourself: *“How have I seen or could I see this concept in action?”*

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