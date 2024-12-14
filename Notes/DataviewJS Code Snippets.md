---
tags:
- obsidian
- dataview
---

## **DataviewJS Code Snippets

### **Summary of DataView JavaScript Snippets for Obsidian**

In this video, several advanced **DataView JavaScript snippets** for **Obsidian** were shared, demonstrating various functionalities for managing and visualizing data from notes. Below is a summary of the key snippets, their functionality, and their configuration details.

#### **1. Tag Cloud**

- **Purpose**: Displays all the tags used in your vault, along with the number of notes associated with each tag.
- **Usage**: Clicking on a tag in the tag cloud takes you to a search view filtered for that tag.
- **Customization**: Requires appropriate CSS to configure the display of tags for better visuals.

#### **2. Page Cloud**

- **Purpose**: Displays all the notes (pages) in your vault in a cloud format.
- **Customization**: Can be configured to display notes from specific folders to avoid performance issues if the vault is large.

#### **3. B Stats**

- **Purpose**: This snippet calculates:
    1. Days since the first note creation.
    2. The total number of notes.
    3. The total number of tags.
- **Display**: Provides a visual representation of these metrics, compatible with both light and dark modes.

#### **4. Habit Tracking with Streaks**

- **Purpose**: Tracks specific habits using metadata properties within daily notes.
- **Configuration Instructions**:
    - **Adjusting Metadata**: Modify the JavaScript code to track habits by specifying the folder and adding properties in the daily note (e.g., `writing`, `exercise`, `reading`).
    - **Habit Criteria**: Set criteria for habits. For example, `if FocusM session > 6`, the habit is marked complete. Use conditional logic in the JavaScript code to set thresholds for goal completion.
    - **Code Changes**: Users with limited coding experience can use AI to assist in customizing these codes for their specific requirements.

#### **5. Habit Tracking (Log Method)**

- **Purpose**: Tracks habits by logging tasks directly in daily notes rather than using metadata properties.
- **Usage**: Users log the habit as a task, such as `- [ ] Day Plan`, in the daily note. This allows habits to be tracked through tasks instead of structured properties.

#### **6. Obsidian Commands List**

- **Purpose**: Lists all the Obsidian commands in the vault.
- **Versions**:
    1. Lists all available commands.
    2. Lists only commands assigned to hotkeys.

#### **7. Progress Tracking**

- **Purpose**: Tracks user-defined metrics (e.g., XP) over time.
- **Customization**:
    - **Set Start and End Dates**: Adjust the code to set a custom date range for tracking progress.
    - **Use Case**: Track metrics such as XP, progress over time, and goal completion.

#### **8. Progress Bar in Table View**

- **Purpose**: Displays a progress bar in a table format.
- **Configuration Instructions**:
    - Create a new note in a "Goals" folder and add properties like `goal`, `progress`, and `deadline`.
    - Modify the DataView JavaScript code to match these properties for visual tracking of goal progress.

#### **9. Book Library Tracking**

- **Purpose**: Create a table view to track books or other types of media, such as movies or TV series.
- **Customization**:
    - **Progress Tracking**: Add a `progress` column to track the percentage of a book read.
    - **CSS Customization**: Use the card-style CSS from the Minimal theme for a more visual book library presentation.

#### **10. Table of Contents**

- **Purpose**: Creates a table of contents (TOC) for all notes in a particular folder.
- **Usage**:
    - The TOC is created by placing a note inside the folder with the same name as the folder itself.
    - The TOC lists all headings from each note, providing a hierarchical outline of all contents in the folder.

#### **11. Alphabetized List**

- **Purpose**: Creates an alphabetical list of all notes in your vault.
- **Usage**: Clicking an alphabet displays all notes starting with that letter.

#### **How to Make Changes and Use AI Assistance**:

1. **Adjusting JavaScript Snippets**:
    - Some snippets (e.g., Habit Tracking, Progress Bar) need code adjustments to fit personal requirements (e.g., folder paths, custom properties).
2. **AI for Customization**:
    - The user can use an AI tool, such as Claude AI, to make these changes by providing the code and describing the desired outcome.
    - AI can help troubleshoot and provide suggestions for modifying JavaScript code to customize habits, goals, or tracking metrics.

#### **Tips for Optimizing Performance**:

- When using snippets like **Tag Cloud** or **Page Cloud**, restrict the query to specific folders if your vault contains a large number of notes, to avoid performance issues.
- Snippets that run on the whole vault may be less efficient, leading to delays or errors, especially with large datasets.

#### **CSS Customization for Visuals**:

- **Card View**: Utilize CSS classes like `cards` to create visually appealing views, such as for books or progress tracking.
- **Minimal Theme**: Extract the card CSS if you're not using the Minimal theme to retain similar visual effects.

#### **Sharing and Resources**:

- The creator has shared the JavaScript snippets and CSS codes in a public Obsidian vault, available on their Patreon page. This includes snippets for various views like tag clouds, page clouds, book libraries, and more.

---

**How-To Key Instructions**:

- **Adding JavaScript Snippets**: To use these JavaScript snippets, paste them into a note in Obsidian and add `dataviewjs` at the beginning.
- **Customization**: For each snippet, adjust folder paths and properties to match your own vault structure.
- **Using AI for Code Adjustments**: If you're unfamiliar with JavaScript, paste the code into an AI tool to get step-by-step guidance or customized versions of the code.

```javascript
// 1. Tag Cloud DataView JS
// Displays all the tags used in your vault, along with their counts.
dataviewjs
let tags = dv.pages().flatMap(p => p.file.tags).reduce((map, tag) => {
    map[tag] = (map[tag] || 0) + 1;
    return map;
}, {});

let sortedTags = Object.keys(tags).sort((a, b) => tags[b] - tags[a]);

dv.container.innerHTML = `
    <div class="tag-cloud">
        ${sortedTags.map(tag => `<span class="tag" style="font-size: ${Math.min(2 + tags[tag] / 10, 5)}em">${tag} (${tags[tag]})</span>`).join('')}
    </div>
`;

// 2. Page Cloud DataView JS
// Displays all the pages in your vault in a cloud format.
dataviewjs
let pages = dv.pages().file.name;

dv.container.innerHTML = `
    <div class="page-cloud">
        ${pages.map(page => `<a href="${page.path}" class="page-link">${page.name}</a>`).join('')}
    </div>
`;

// 3. Habit Tracking with Streaks DataView JS
// Tracks specific habits using properties defined in daily notes.
dataviewjs
let habits = ["writing", "exercise", "reading"];  // List of habits to track
let habitData = dv.pages('"reflect"') // Use pages in the "reflect" folder
    .where(p => habits.some(h => p[h]))
    .map(p => ({
        date: p.file.day,
        habits: habits.map(h => p[h] ? "✔️" : "❌")
    }));

habitData.forEach(h => {
    dv.header(3, h.date.toFormat("yyyy-MM-dd"));
    dv.list(h.habits.map((done, i) => `${habits[i]}: ${done}`));
});

// 4. Progress Bar in Table View DataView JS
// Creates a progress bar for tracking goals in a table view.
dataviewjs
let goals = dv.pages('"goals"')
    .map(goal => ({
        name: goal.goal,
        progress: Math.min(Math.max(goal.progress, 0), 100) // Bound progress between 0-100
    }));

dv.table(["Goal", "Progress"], 
    goals.map(g => [g.name, `
        <div class="progress-bar" style="width: 100px; background: #ccc;">
            <div style="width: ${g.progress}%; background: #4caf50;">${g.progress}%</div>
        </div>
    `])
);

// 5. Book Library Tracking DataView JS
// Tracks the books you've read and shows the progress for each one.
dataviewjs
let books = dv.pages('"books"')  // Replace "books" with your folder name if different
    .map(book => ({
        title: book.title,
        totalPages: book.totalPage,
        currentPage: book.currentPage,
        progress: Math.round((book.currentPage / book.totalPage) * 100)
    }));

dv.table(["Title", "Progress"], 
    books.map(b => [b.title, `
        <div class="progress-bar" style="width: 100px; background: #ccc;">
            <div style="width: ${b.progress}%; background: #4caf50;">${b.progress}%</div>
        </div>
    `])
);

// 6. Obsidian Commands List DataView JS
// Lists all commands in your vault, or only those assigned to hotkeys.
dataviewjs
const commands = app.commands.listCommands();
let allCommands = commands.map(c => ({name: c.name, id: c.id}));
let hotkeyCommands = commands.filter(c => c.hotkeys.length > 0);

dv.table(["Command", "ID"], allCommands.map(cmd => [cmd.name, cmd.id]));
dv.header(3, "Commands with Hotkeys");
dv.list(hotkeyCommands.map(cmd => `${cmd.name}: ${cmd.hotkeys.join(", ")}`));
```

[[Obsidian]]