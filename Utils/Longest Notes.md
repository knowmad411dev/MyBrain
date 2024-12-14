---
tags:
- dataview
---

## **Longest Notes

```dataviewjs
const bwc = app.plugins.plugins["better-word-count"].api; // Access the Better Word Count plugin's API
const luxon = dv.luxon;

// Get all pages in the vault, ensure they are markdown, exclude "excalidraw.md"
const pages = await dv.pages('""').where(page => page.file.ext === "md" && page.file.path.endsWith("excalidraw.md") == false);

// Array to store the final rows for the table
const tableRows = [];

// Use Promise.all to wait for all word counts
await Promise.all(pages.map(async (page) => {
    const wordCount = await bwc.getWordCountPagePath(page.file.path); // Get word count for the page using Better Word Count plugin
    page.wordCount = wordCount; // Add the word count as a property to the page object
}));

// Create a new array that is sorted
const sortedPages = [...pages].sort((pageA, pageB) => pageB.wordCount - pageA.wordCount);

// Iterate through the sorted pages and add rows to the tableRows array
const numberOfNotesToShow = 10; // Number of largest notes to display
for (let i = 0; i < numberOfNotesToShow && i < sortedPages.length; i++) {
    const page = sortedPages[i];
    const wordCount = page.wordCount;
    const relativeModified = luxon.DateTime.fromISO(page.file.mtime).toRelative();

    tableRows.push([
        page.file.link,
        wordCount,
        relativeModified,
    ]);
}

// Print the table with the top notes based on word count
dv.table(["Name", "Word Count", "Last modified"], tableRows);
```

[[Obsidian]]