---
date: 2024-12-09>)
tags:
- dataview
title: TopicsIndex
---

[[Obsidian Dataview Overview]]
```dataviewjs
// Collect all notes
const notes = dv.pages("").sort(n => n.file.name, "asc");

// Group notes by inferred "topic" (tags or folder)
const groupedNotes = notes.groupBy(note => {
    // Use the first tag if tags exist, otherwise use the folder name
    let topic = note.tags && Array.isArray(note.tags) ? note.tags[0] : note.file.folder || "Unsorted";
    return topic.length === 1 ? "Invalid Group" : topic; // Skip single-character group names
});

// Display the grouped notes
for (let group of groupedNotes) {
    if (group.key === "Invalid Group") continue; // Skip invalid groups
    dv.header(2, group.key); // Topic or folder name
    dv.list(group.rows.map(note => `[[${note.file.name}]]`)); // Links to notes
}
```