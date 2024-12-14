---
tags:
- obsidian
video-url: https://www.youtube.com/watch?v=yhr-6A2v_Tc&list=WL&index=2
---

## **Mastering Obsidian Templates

**Title: Obsidian Templates Overview with Paul**

**Introduction:**
- Paul introduces himself and shares that in this video, he will be exploring **Obsidian templates and workflows**.
- The focus is on using templates effectively and showing advanced techniques with the **Templater** and **QuickAdd** plugins to fully utilize **Obsidian**.

**Importance of Templates in Obsidian:**
- Templates are essential for anyone who takes extensive notes or manages multiple topics.
- They can **greatly enhance efficiency** by saving users time, especially for repetitive tasks.
- Templates help maintain **consistency** by including reusable elements like:
  - **YAML properties** for metadata.
  - **Headings** for structured note-taking.
  - **Text snippets** that are commonly reused.

**Examples of Templates Usage:**
- Paul shares that he uses templates for various purposes, such as:
  - **Daily Notes**: Keeping track of everyday thoughts and activities.
  - **Book Reviews**: Organizing reviews with specific properties like **rating** and **status**.
  - **Learning from YouTube Videos**: Summarizing information learned.
  - **Concepts and Ideas**: Documenting new ideas and topics.

**Showcasing Templates and Workflow:**
- Paul takes viewers through his **Templates Directory**:
  - He stores all templates in a directory within his Obsidian Vault called "Templates."
  - He has another folder for **Templater scripts** that automate tasks.
- He demonstrates accessing the templates folder, showing over **50 different templates**, and talks about organizing them for easy use.

**Creating a New Template:**
- To create a new template, Paul can navigate to the templates directory or use a "New Template" button he has configured.
- **Minimal Template Example**:
  ```yaml
  ---
  date: <% tp.date.now("YYYY-MM-DD") %>
  css_classes:
  tags: []
  aliases: []
  summary: ""
  type: ""
  status: "Draft"
  related: []
  ---
  ```
  - **YAML properties** include:
    - **Date**: Uses Templater to insert the current date.
    - **Tags, Aliases, Summary**: Metadata placeholders.
    - **Status**: Set to "Draft" by default.
  - **CSS Classes**: For custom styling.

**Benefits and Challenges of Templates:**
- When starting with Obsidian, Paul admits he didn’t understand the **value of templates** and lacked consistency in his notes.
- **Dynamic Content** in templates, like **Templater scripts**, initially felt intimidating due to the learning curve, but he found them to be very beneficial.

**Examples of Templates and Templater Scripts**:

1. **Ideas Template**:
   ```yaml
   ---
   date: <% tp.date.now("YYYY-MM-DD") %>
   tags: [#idea, 💡, 🌱]
   status: "In Progress"
   category: "Ideas"
   ---
   ## Summary
   - Topic:
   - Source:

   > [!meta]- Meta Details
   This section includes metadata details for easy tracking.
   ```
   - **YAML properties**:
     - **Date**: Inserted automatically using Templater.
     - **Tags**: Includes hashtags like "idea," a light bulb emoji, and a seedling emoji.
     - **Status**: Set to "In Progress".
     - **Category**: Set to "Ideas".
   - Includes **Summary** and **Source** sections for clarity.

2. **Book Review Template**:
   ```yaml
   ---
   date: <% tp.date.now("YYYY-MM-DD") %>
   book_title: ""
   author: ""
   rating: <% tp.system.suggester(["⭐ 1", "⭐⭐ 2", "⭐⭐⭐ 3", "⭐⭐⭐⭐ 4", "⭐⭐⭐⭐⭐ 5"], ["1", "2", "3", "4", "5"]) %>
   format: <% tp.system.prompt("eBook, Paperback, Audiobook?") %>
   status: <% tp.system.suggester(["Not Started", "In Progress", "Completed"], ["Not Started", "In Progress", "Completed"]) %>
   ---
   ## Summary
   - Key Insights:

   > [!meta]- Meta Details
   - Additional thoughts and impressions about the book.
   ```
   - **Rating**: Uses Templater to prompt the user for a rating, offering **five-star options**.
   - **Format**: Prompts the user to specify if the book is an **eBook, Paperback, or Audiobook**.
   - **Status**: Asks for the reading status.

3. **Tools Template**:
   ```yaml
   ---
   date: <% tp.date.now("YYYY-MM-DD") %>
   tags: [#tool]
   ---
   ## Tool Overview
   - Name:
   - Use Case:
   - Category:

   > [!meta]- Meta Details
   - Documentation Link:
   ```
   - Consistent format for all **tools-related** notes, with fields for the **tool's name, use case**, and **category**.

**Applying Templates in Obsidian**:
- **Default Method**:
  - Create a new note (`Ctrl + N`), and then apply the template (`Ctrl + P` and select template).
  - To execute **Templater Snippets**, Paul uses `Ctrl + P` and selects "Replace Templates in Active File."
  - **Issue**: New notes are placed in the **generic Notes Lab**, requiring manual movement to the appropriate folder.

**Using QuickAdd Plugin for Templates**:
- Paul explains that **QuickAdd** enhances the process of applying templates:
  - **QuickAdd** allows users to:
    - Select the **template**.
    - Specify the **folder** for the note.
    - Automatically execute **Templater scripts**.
  - Example:
    - **New Idea Note**:
      - **Name Prompt**: Prompts for the note's name.
      - **Folder Placement**: Automatically saved to the **"Ideas" folder**.
      - **Dynamic Elements**: Templater script runs automatically, filling in details.

**Using Templater Scripts for Automation**:
- **Templater Script Example**:
  - **Prompt for File Name and Move to Folder**:
    ```javascript
    <%*
    const note_name = await tp.system.prompt("Enter note name");
    const folder = "02 Cards";
    await tp.file.rename(note_name);
    await tp.file.move(`${folder}/${note_name}`);
    %>
    ```
  - Prompts for a **note name**, then moves the note to a specific folder in the vault (e.g., **"02 Cards" folder**).
  - This script provides flexibility without requiring **QuickAdd**.

**Folder Templates**:
- **Folder-Specific Templates**:
  - Enable folder templates in **Templater settings**, which allows a specific template to be applied automatically when creating a note in a certain folder.
  - Example:
    - Creating a note in the **"Cards Ideas"** folder automatically applies the **Ideas Template**.

**Template Hotkeys**:
- Templates can be used with **hotkeys**:
  - **Slash Commands**:
    - Example: Using a **slash command** to insert a quote callout in a note.
    ```markdown
    > [!quote] Quote: "The only way to do great work is to love what you do." — Steve Jobs
    ```

**Using Templater for Automation**:
- Paul uses Templater to create dynamic content:
  - **Templater Example**:
    ```yaml
    ---
    date_added: <% tp.date.now("dddd, MMMM Do YYYY") %>
    random_note: <% tp.file.cursor(0) %>
    ---
    ```
    - **Date Added**: Dynamically inserts today’s date.
    - **Random Note**: Uses Dataview queries to pull a random note from the vault.

**Setting Up Templates in Obsidian**:
- To set up templates:
  - Define the **Templates Folder** in Core Plugin settings.
  - Install the required community plugins (**Commander**, **QuickAdd**, and **Templater**).
  - Create a **Default Template** with common properties, dynamic dates, tags, and metadata details.

**Using QuickAdd for Note Creation**:
- Paul demonstrates how to create notes using **QuickAdd**:
  - **Add Choice** in QuickAdd to specify the template and folder for new notes.
  - Example:
    - Create a **"Concept Template Note"** in the "Concepts" folder, using the specified template automatically.

**Hotkey Customization for Note Creation**:
- Paul customizes the hotkey:
  - Reassign **"Ctrl + N"** to use QuickAdd instead of creating a new untitled note.
  - This helps keep the vault organized by ensuring that new notes have predefined templates.

**Dynamic Content with Templater**:
- Adding **dynamic content** to the **Default Template**:
  ```yaml
  ---
  date: <% tp.date.now("YYYY-MM-DD") %>
  tags: [🌱]
  status: "In Progress"
  ---
  ## Random Note of the Day
  <% tp.random.choice(await dv.pages()) %>

  ## Files Created Today
  - <%* tp.file.list("date", "created today") %>

  ## Files Modified Today
  - <%* tp.file.list("date", "modified today") %>
  ```
  - **Random Note**: Uses Templater to display a randomly selected note from the vault.
  - **Files Created/Modified Today**: Uses Templater and **Dataview** to create a list of recently created or modified files.

**Summary and Conclusion**:
- **Templater** and **QuickAdd** are powerful plugins that automate repetitive tasks, making workflows more efficient.
- Paul encourages viewers to explore different approaches and find what works best for them. He also emphasizes that it’s normal to adjust and modify templates over time.
- The **Obsidian Starter Kit Vault** is available on Paul’s **Ko-Fi** page to help viewers follow along.

---

This overview includes detailed examples of Paul's **templates** and **Templater scripts**, illustrating how these elements contribute to more streamlined note-taking and consistency in Obsidian. Templates are fundamental in enhancing workflows, and plugins like Templater and QuickAdd provide powerful automation capabilities.

[[Obsidian]]  [[Obsidian YAML]]
