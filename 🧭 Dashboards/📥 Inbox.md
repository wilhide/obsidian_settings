---
obsidianUIMode: preview
---
# 📥 Inbox Dashboard

> [!info] Capture Processing
> - Review each open capture below, promote the contents to the right project or knowledge note, then flip `processed` to `true`.
> - Run your archive macro periodically to move closed captures out of `📥 Inbox/`.

## 📝 Open Captures
```dataviewjs
const MAX_PREVIEW = 180; // tweak this value to change snippet length
const openPages = dv.pages("\"📥 Inbox\"")
  .where(p => p.processed === false)
  .sort(p => p.created ? -p.created.toMillis() : 0);

const openRows = [];
for (const page of openPages) {
  const raw = await dv.io.load(page.file.path);
  const withoutFrontmatter = raw.replace(/^---[\s\S]*?---\s*/, "");
  const singleLine = withoutFrontmatter.replace(/\n/g, " ").trim();
  const preview = singleLine.length > MAX_PREVIEW
    ? singleLine.substring(0, MAX_PREVIEW) + "…"
    : singleLine;
  openRows.push([page.file.link, preview]);
}

dv.table(["Capture", "Preview"], openRows);
```

## ✅ Recently Closed
```dataviewjs
const MAX_PREVIEW = 180; // tweak this value to change snippet length
const closedPages = dv.pages("\"📥 Inbox\"")
  .where(p => p.processed === true)
  .sort(p => p.created ? -p.created.toMillis() : 0)
  .limit(10);

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

> [!tip] Adjust Preview Length
> Update `MAX_PREVIEW` in either DataviewJS block above to show more or less of each capture’s body.
