Automatically moves processed inbox items into the archive.
```javascript
/**
 * Archive_Inbox.js
 *
 * QuickAdd macro helper for the Kind Mind vault.
 * - Moves every capture note in `📥 Inbox/` whose frontmatter has `processed: true`
 *   into `🗄️ Archive/Inbox Archive/`, ensuring filenames remain unique.
 * - Permanently deletes captures older than 30 days so the archive stays trim.
 * - Intended to be called by the “Archive Processed Captures” QuickAdd macro.
 */

module.exports = async (params) => {
  const { app } = params;
  const { vault, metadataCache } = app;
  const moment = window.moment;

  const SOURCE_FOLDER = "📥 Inbox";
  const ARCHIVE_FOLDER = "🗄️ Archive/Inbox Archive";
  const DELETE_CUTOFF_DAYS = 30;

  const ensureFolder = async (path) => {
    let folder = vault.getAbstractFileByPath(path);
    if (!folder) {
      await vault.createFolder(path);
      folder = vault.getAbstractFileByPath(path);
    }
    return folder;
  };

  const gatherMarkdownFiles = (folder, bucket = []) => {
    for (const child of folder.children) {
      if (child.children) {
        gatherMarkdownFiles(child, bucket);
      } else if (child.extension === "md") {
        bucket.push(child);
      }
    }
    return bucket;
  };

  const uniquePath = (base, name) => {
    const stem = name.replace(/\.md$/i, "");
    const ext = name.endsWith(".md") ? ".md" : "";
    let i = 1;
    let candidate = `${base}/${name}`;
    while (vault.getAbstractFileByPath(candidate)) {
      candidate = `${base}/${stem} ${i}${ext}`;
      i += 1;
    }
    return candidate;
  };

  const sourceFolder = vault.getAbstractFileByPath(SOURCE_FOLDER);
  if (!sourceFolder || !sourceFolder.children) {
    new Notice(`Archive macro: folder "${SOURCE_FOLDER}" not found.`);
    return;
  }

  await ensureFolder(ARCHIVE_FOLDER);
  const allCaptureFiles = gatherMarkdownFiles(sourceFolder);

  let moved = 0;
  let deleted = 0;
  const now = moment();

  for (const file of allCaptureFiles) {
    if (file.path.startsWith(`${ARCHIVE_FOLDER}/`)) continue;

    const cache = metadataCache.getFileCache(file);
    const frontmatter = cache?.frontmatter;
    if (!frontmatter || frontmatter.processed !== true) continue;

    const createdRaw = frontmatter.created;
    const created = createdRaw ? moment(createdRaw) : null;
    const isOlderThanCutoff =
      created && now.diff(created, "days") > DELETE_CUTOFF_DAYS;

    if (isOlderThanCutoff) {
      await vault.trash(file, true); // true => skip system trash
      deleted += 1;
    } else {
      const targetPath = uniquePath(ARCHIVE_FOLDER, file.name);
      await vault.rename(file, targetPath);
      moved += 1;
    }
  }

  new Notice(
    `Archive macro finished: ${moved} moved, ${deleted} deleted (>${DELETE_CUTOFF_DAYS} days).`
  );
};
```