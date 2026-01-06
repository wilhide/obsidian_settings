---
type: dashboard
tags:
  - dashboard
  - area/professional
---
# 🧠 People by SME Area

```dataviewjs
// ===== CONFIGURATION =====
const PEOPLE_PATH = "🧠 Knowledge Base/👤 People";
const UNASSIGNED = "#sme/unassigned";

// ===== LOAD PEOPLE =====
const pages = dv.pages(`"${PEOPLE_PATH}"`);

// Map: smeTag -> [pages]
const groups = new Map();

for (const p of pages) {
  const tags = (p.file?.tags ?? []).map(t => String(t));

  // Extract SME tags
  const smeTags = tags.filter(t => t.startsWith("#sme/"));

  const effectiveTags = smeTags.length ? smeTags : [UNASSIGNED];

  for (const tag of effectiveTags) {
    if (!groups.has(tag)) groups.set(tag, []);
    groups.get(tag).push(p);
  }
}

// Sort SME areas alphabetically
const sortedTags = Array.from(groups.keys()).sort((a, b) =>
  a.localeCompare(b)
);

// ===== RENDER =====
for (const tag of sortedTags) {
  const people = groups
    .get(tag)
    .sort((a, b) => a.file.name.localeCompare(b.file.name));

  dv.header(3, tag);

  if (tag === UNASSIGNED) {
    dv.paragraph("> ⚠️ These people do not yet have any `#sme/*` tags.");
  }

  dv.list(
    people.map(p => {
      const role = p.role ? ` — ${p.role}` : "";
      return `${p.file.link}${role}`;
    })
  );
}
```