# 🧠 Knowledge Dashboard

> [!tip] Capture → Process → Grow  
> - Save cool ideas to the **📥 Inbox**.  
> - During your review, summarize and move them here.  
> - Optional: Add a quick **💭 Personal Reflection** if it resonates.


## ✨ Recently Updated Notes
```dataview
TABLE file.link AS "Note", file.mtime AS "Last Edited"
FROM "🧠 Knowledge Base"
SORT file.mtime DESC
LIMIT 10
```

## 📘 Most Referenced Notes
```dataview
TABLE file.link AS "Topic", length(file.inlinks) AS "Linked From"
FROM "🧠 Knowledge Base"
SORT length(file.inlinks) DESC
LIMIT 10
```

## 🧩 Random Note to Revisit
```dataview
TABLE file.link AS "Note"
FROM "🧠 Knowledge Base"
SORT file.mtime DESC
LIMIT 1
```
