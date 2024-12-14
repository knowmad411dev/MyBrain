---
tags:
- dataview
---

[[Obsidian]]

```dataviewjs
// Initialize a Map to store the total frequency of links across the vault
let linkFrequency = new Map();

// Iterate over all pages in the vault
for (let page of dv.pages()) {
    // Skip pages from the "Attachments" folder
    if (page.file.path.includes("Attachments")) continue;

    // Access the content of each page
    const content = await app.vault.read(app.vault.getAbstractFileByPath(page.file.path));
    
    // Match all [[links]] in the content
    const links = content.match(/\[\[([^\]]+)\]\]/g);
    if (links) {
        links.forEach(link => {
            const cleanLink = link.replace(/^\[\[|\]\]$/g, "").trim(); // Remove [[ and ]]
            
            // Skip links to images based on common image extensions
            if (/\.(png|jpg|jpeg|gif|svg|bmp|webp)$/i.test(cleanLink)) return;
            
            // Increment total frequency
            linkFrequency.set(cleanLink, (linkFrequency.get(cleanLink) || 0) + 1);
        });
    }
}

// Convert the Map to an array and sort it by frequency (descending)
const sortedLinks = Array.from(linkFrequency.entries()).sort((a, b) => b[1] - a[1]);

// Render the table
dv.table(["Link", "Frequency"], sortedLinks.map(([link, freq]) => [`[[${link}]]`, freq]));
```

``