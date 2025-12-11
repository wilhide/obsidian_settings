---
type: concept | howto | playbook | pattern | research
tags:
  - knowledge
  - area/professional
title:
summary:
last_reviewed:
  "{ date:YYYY-MM-DD }":
related: []
sources: []
poc:
---
> [!info] Knowledge Capture Flow  
> - Start with a short **Summary** of what you learned.  
> - Add **Reflection** only if you feel inspired.  
> - Tag with `#reference` or `#idea` to surface on dashboards.
> - Types
> 	- **concept**: Capture _understanding_ — what something _is_, _how it works_, and _why it matters_.
> 	- **howto**: Capture _procedural_ knowledge — step-by-step instructions for doing something.
> 	- **playbook**: Capture _situational workflows_ — structured responses to recurring scenarios that mix _decision-making + action._
> 	- **pattern**: Capture _reusable solution templates_ — generalizable structures that solve a recurring problem.
> 	- **research**: Capture _source material_ and distilled insights from reading, courses, or experiments.


# 📝 Summary
(Brief notes or key takeaways)

# 💭 Personal Reflection (optional)
(Why this matters to me / how I might apply it)

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