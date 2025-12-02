# 🧭 Today Dashboard

## 📅 Today’s Note
Today: `= link(dateformat(date(today), "yyyy-MM-dd"), dateformat(date(today), "cccc, LLL d"))` | Yesterday: `= link(dateformat(date(today) - dur(1 day), "yyyy-MM-dd"), dateformat(date(today) - dur(1 day), "cccc, LLL d"))`


> [!tip] Daily Flow Reminder  
> 1️⃣ Check **Focus & Priorities** in your daily note.  
> 2️⃣ Knock out 1–2 quick wins.  
> 3️⃣ Add anything new to the **📥 Inbox** — don’t organize yet!  
> 4️⃣ Reflect for 2 minutes before closing Obsidian.

## ⭐ Favorites
- [[🧭 Dashboards/📥 Inbox|📥 Inbox Dashboard]]
- [[💼 Projects|💼 Projects Dashboard]]
- [[🧠 Knowledge|🧠 Knowledge Dashboard]]

## 📥 Recent Captures
```dataviewjs
const MAX_PREVIEW = 180; // tweak this value to change snippet length
const closedPages = dv.pages("\"📥 Inbox\"")
  .where(p => p.processed === false)
  .sort(p => p.created ? -p.created.toMillis() : 0)
  .limit(5);

const closedRows = [];
for (const page of closedPages) {
  const raw = await dv.io.load(page.file.path);
  const withoutFrontmatter = raw.replace(/^---[\s\S]*?---\s*/, "");
  const singleLine = withoutFrontmatter.replace(/\n/g, " ").trim();
  const preview = singleLine.length > MAX_PREVIEW
    ? singleLine.substring(0, MAX_PREVIEW) + "…"
    : singleLine;
  closedRows.push([page.file.link, preview]);
}

dv.table(["Capture", "Preview"], closedRows);
```

## ⏳ Waiting On
```tasks
not done
path includes 💼 Projects
description includes #waiting
limit 5
group by filename
hide backlinks
exclude sub-items
```

## 🔥 Active Projects
```dataview
TABLE status AS "Status", due AS "Due"
FROM "💼 Projects"
WHERE contains(tags, "project") AND !contains(tags, "complete")
SORT due ASC
LIMIT 5
```

## 🧠 Random Knowledge to Revisit
```dataview
TABLE file.link AS "Note"
FROM "🧠 Knowledge Base"
SORT file.mtime DESC
LIMIT 1
```

