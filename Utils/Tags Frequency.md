---
tags:
- dataview
---

[[find tags]]   [[Obsidian]]

## **Tags Frequency

```dataviewjs
// DataviewJS to list and sort tag occurrences from YAML frontmatter alphabetically
let tagCounts = {}; // Initialize an empty object to store tag counts

// Retrieve all pages in the vault
let pages = dv.pages();

// Iterate over each page to extract and count tags from YAML frontmatter
pages.forEach(page => {
  if (page.file.frontmatter && page.file.frontmatter.tags) {
    // Ensure tags are in array format, or convert to array if it's a single string
    let tags = Array.isArray(page.file.frontmatter.tags) 
      ? page.file.frontmatter.tags 
      : [page.file.frontmatter.tags];

    // Count each tag
    tags.forEach(tag => {
      if (!tagCounts[tag]) {
        tagCounts[tag] = 0; // Initialize count for the tag
      }
      tagCounts[tag]++; // Increment the count for each occurrence
    });
  }
});

// Sort tags alphabetically
let sortedTags = Object.entries(tagCounts).sort((a, b) => a[0].localeCompare(b[0]));

// Display the sorted results in a table
dv.table(
  ["Tag", "Occurrences"], 
  sortedTags.map(([tag, count]) => [tag, count])
);
```