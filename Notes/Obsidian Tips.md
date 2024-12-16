---
tags:
- obsidian
- dataview
video-url: https://www.youtube.com/watch?v=3qopiej4Zo0&list=WL&index=2
---

## **Obsidian Tips

**Obsidian Customization Tips: Overview and How-To Guide**

### **1. Formatting Notes with CSS Columns**

**Purpose:** Split note text into two or three columns for better readability.

**Steps:**
1. **Enable CSS Snippets in Obsidian:**
   - Go to `Settings > Appearance > CSS Snippets`.
   - Click the folder icon to open the snippets folder.
   - Create a new file called `columns.css`.

2. **Add CSS Code:**
   - Copy CSS code (from the linked resource) into `columns.css`.
   - Save the file.

3. **Activate the Snippet:**
   - Return to Obsidian.
   - Refresh the snippets and enable the new snippet.

4. **Apply the Layout:**
   - Add the property `cssclasses` to the note.
   - Assign the value `columns2` (for two columns) or `columns3` (for three columns).
   - Switch to Reading View (`CTRL+E`) to see the columns applied.

**Key CSS Classes:**
- `.columns2`: Defines a two-column layout.
- `.columns3`: Defines a three-column layout.

---

### **2. Floating Callouts**

**Purpose:** Allow callouts to float left or right, saving space and improving aesthetics.

**Steps:**
1. **Add a CSS Snippet:**
   - Create a file named `embedded_callouts.css`.
   - Enable the snippet in Obsidian as described in step 1 above.

2. **CSS Classes:**
   - `float-r`: Aligns callouts to the right.
   - `float-l`: Aligns callouts to the left.

3. **Use in Notes:**
   - Add the `|float-r` or `|float-l` directly to the callout type, e.g., `> [!important|float-r]`.

4. **Optional:** Enable folding for callouts to minimize them when not in use.

---

### **3. Custom Table Styles**

**Purpose:** Apply predefined or custom styles to tables within notes.

**Steps:**
1. **Enable Table Styling Snippet:**
   - Add a CSS file with table styles (e.g., `custom_tables.css`).
   - Enable the snippet.

2. **Select a Style:**
   - Add the `cssclasses` property to a note.
   - Assign one of the provided styles (e.g., `purpleRed`, `academia`).

3. **Customization:**
   - Modify CSS directly to adjust width, alignment, cell sizes, or colors.

---

### **4. Tasks Dashboard**

**Purpose:** Create a dashboard showing tasks grouped by due dates.

**Requirements:**
- **Plugins:** Tasks plugin, MCL Multicolumn CSS.

**Steps:**
1. **Set Up Task Queries:**
   - Use the Tasks plugin to define queries for tasks:
     - Overdue: Due before today.
     - Due today: Sort by priority.
     - Due this week: Due after today but within the week.
     - Due later: Due after this week.

2. **Format Queries:**
   - Add compact formatting by hiding the edit button, backlink, and task count.

3. **Align Queries:**
   - Wrap each query in a callout (`CTRL+P > Insert Callout`) and group them into columns using the multicolumn layout.

---

### **5. Finding Longest Notes**

**Purpose:** List the top 10 longest notes in the vault.

**Requirements:**
- **Plugins:** Dataview, Better Word Count.

**Steps:**
1. **DataviewJS Script:**
   ```javascript
   const notes = dv.pages().filter(p => p.file.name !== "excalidraw.md");
   const withWordCounts = notes.map(n => ({
       name: n.file.name,
       wordCount: app.plugins.plugins["better-word-count"].api.getWordCount(n.file.path),
       lastModified: n.file.mtime
   }));
   const sortedNotes = withWordCounts.sort((a, b) => b.wordCount - a.wordCount).slice(0, 10);
   dv.table(["Note Name", "Word Count", "Last Modified"], sortedNotes.map(n => [n.name, n.wordCount, n.lastModified]));
   ```

2. **Output:** Generates a table showing note name (with links), word count, and last modified date.

---

### **6. Tooltip for Help**

**Purpose:** Create a help tooltip that appears when hovering over a specific icon.

**Steps:**
1. **Create a CSS Snippet:**
   - Add a file named `help_tooltip.css`.
   - Define the tooltip appearance and encode the image (optional).

2. **Encoding Images:**
   - Convert an SVG image into a CSS-compatible string using tools like `csspro`.

3. **Activate and Test:**
   - Enable the CSS snippet and verify the tooltip's behavior in Obsidian.

---

### **7. Adding Logos or Backgrounds**

**Purpose:** Display a custom logo or background when no note is open.

**Steps:**
1. **Create a Snippet (`empty_note_logo.css`):**
   - Encode the logo and define its positioning.

2. **Enable the Snippet:**
   - Apply it to display the logo in the empty state or a specific area.

---

### **8. Enhanced Web Clipper Templates**

**Purpose:** Capture web content with customizable templates.

**Features:**
- Predefined templates for platforms like Twitter, Wikipedia, Reddit, Medium, and YouTube.
- Templates include metadata like URLs, timestamps, descriptions, or transcripts.

**Customization:**
- Modify templates for specific formatting or use cases.

---

### **9. Acknowledging the Community**

**Purpose:** Highlight the importance of user-generated content for enhancing Obsidian's capabilities.

**Note:**
- Many tweaks, plugins, and themes are shared by users on forums, Reddit, and Discord.

**Suggestion:** Explore these resources for inspiration and additional features.

---

This summary outlines the detailed processes for implementing each feature and using Obsidian plugins effectively. Let me know if you need further clarification or help with specific code!

[[Obsidian]]