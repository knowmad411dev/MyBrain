---
tags:
- dataview
---

[[Obsidian]]

```dataviewjs
const pages = dv.pages().filter(p => p.tags && !p.file.path.includes("Images"));

dv.table(["File", "Tags"], pages.map(p => [    p.file.link,    Array.isArray(p.tags) ? p.tags.join(", ") : p.tags ? p.tags : ""]));
```
