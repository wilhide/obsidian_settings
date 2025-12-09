# 💼 Projects Dashboard

> [!note] How to Use This Dashboard  
> - Each project = 1 note in 💼 **Projects**.  
> - Update `status::`, `due::`, and `next_step::` in each note.  
> - Tag active ones with `#project`.  
> - When finished, tag it `#complete` to archive automatically.

## 🟢 Active Projects
```dataview
TABLE status AS "Status", due AS "Due"
FROM "💼 Projects"
WHERE contains(tags, "project") AND !contains(tags, "complete") AND !contains(status, "On Hold")
SORT due ASC
```

## ⚪ On Hold / Someday
```dataview
TABLE status AS "Status", due AS "Due"
FROM "💼 Projects"
WHERE contains(tags, "project") AND contains(status, "On Hold")
```

## 🔴 Completed Projects
```dataview
TABLE file.link AS "Project", file.mtime AS "Completed On"
FROM "💼 Projects"
WHERE contains(tags, "complete")
SORT file.mtime DESC
```
