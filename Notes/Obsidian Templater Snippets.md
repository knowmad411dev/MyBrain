---
tags:
- obsidian
video-url: https://www.youtube.com/watch?v=9w_BQHH3ptY&list=WL&index=17
---

# Mastering Obsidian Templater Plugin: Advanced Snippets and Automation

The Templater plugin for Obsidian is a powerful tool that extends the native templating capabilities of Obsidian. While many users utilize it for basic templating, Templater offers advanced functions that can significantly streamline your workflow by automating repetitive tasks. This guide provides a comprehensive overview of some of the best Templater snippets, ranging from simple date insertions to advanced automation scripts.

## Getting Started with Templater

To begin using these snippets, you'll need to install the Templater plugin:

1. Open Obsidian's **Settings**.
2. Navigate to **Community Plugins** and turn off **Safe Mode**.
3. Click on **Browse** and search for **Templater**.
4. Install and enable the plugin.
5. In **Settings** > **Templater**, set your **Template folder location** (e.g., `Templates`).
6. Enable **Trigger Templater on new file creation** for automatic template application.

---

## Basic Templater Snippets

### Inserting Today's Date

Create a new template file in your Templates folder named `Date.md` and add the following snippet:

```Templater
<% tp.date.now("DD-MM-YYYY") %>
```

- **Usage**: Inserts today's date in the format `DD-MM-YYYY`.
- **Example Output**: `12-01-2024`.

#### Custom Date Format

You can customize the date format. For example:

```Templater
<% tp.date.now("YYYY-MM-DD") %>
```

- **Example Output**: `2024-01-12`.

### Date Formats Reference

For custom date formats, refer to the Moment.js documentation under the **Display** section.

---

## Advanced Date Functions

### Date from Note's Title

If your note titles are dates, you can extract and format the date from the title:

```Templater
<% tp.date.extract(tp.file.title, "YYYY-MM-DD").format("dddd, MMMM Do YYYY") %>
```

- **Usage**: Converts a date in the note's title to a formatted date within the note.
- **Example**: If your note is titled `2024-01-12`, the output will be `Friday, January 12th 2024`.

### Navigating Between Daily Notes

Create navigation links between your daily notes:

```Templater
[[<% tp.date.yesterday("YYYY-MM-DD") %>|Yesterday]] | [[<% tp.date.tomorrow("YYYY-MM-DD") %>|Tomorrow]]
```

- **Usage**: Places links to yesterday's and tomorrow's daily notes.
- **Note**: Ensure your daily notes follow the `YYYY-MM-DD` format.

### Day of the Year

Display the day number within the year:

```Templater
Day <% tp.date.now("DDD") %> of the year
```

- **Example Output**: `Day 12 of the year`.

---

## Periodic Notes Automation

### Weekly Note Navigation

For weekly notes, you can create navigation between weeks:

```Templater
[[<% tp.date.now("gggg-[W]WW", -1, "week") %>|Last Week]] | [[<% tp.date.now("gggg-[W]WW", +1, "week") %>|Next Week]]
```

- **Usage**: Places links to last week's and next week's notes.

### Listing Daily Notes in a Week

Automatically list all daily notes within a week:

```Templater
<%* let startOfWeek = tp.date.now("YYYY-MM-DD", 0, "week"); for (let i = 0; i < 7; i++) {   let date = moment(startOfWeek).add(i, 'days').format("YYYY-MM-DD");   tR += `- [[${date}]]\n`; } %>
```

- **Usage**: Generates a list of links to each day's note for the current week.

---

## Automating Note Creation

### Automatic Periodic Notes Creation

Automatically create daily, weekly, monthly, and yearly notes if they don't exist:

```Templater
<%* // Define the date formats
const dailyFormat = "YYYY-MM-DD";
const weeklyFormat = "gggg-[W]WW";
const monthlyFormat = "YYYY-MM";
const yearlyFormat = "YYYY";

// Get the paths
const dailyPath = `Daily Notes/${tp.date.now(dailyFormat)}.md`;
const weeklyPath = `Weekly Notes/${tp.date.now(weeklyFormat)}.md`;
const monthlyPath = `Monthly Notes/${tp.date.now(monthlyFormat)}.md`;
const yearlyPath = `Yearly Notes/${tp.date.now(yearlyFormat)}.md`;

// Create notes if they don't exist
await tp.file.create_new(dailyPath);
await tp.file.create_new(weeklyPath);
await tp.file.create_new(monthlyPath);
await tp.file.create_new(yearlyPath);
%>
```

- **Usage**: Place this in a template to automatically generate periodic notes.

---

## Utility Snippets

### Important Dates Countdown

Keep track of upcoming events:

```Templater
<%* let eventDate = moment("2024-12-31", "YYYY-MM-DD"); let today = moment(); let daysLeft = eventDate.diff(today, 'days'); tR += `🎉 ${daysLeft} days left until New Year's Eve!`; %>
```

- **Usage**: Adjust the `eventDate` to your target date.

### Display File Title as Heading

Automatically insert the file's title as a heading:

```Templater
# <% tp.file.title %>
```

- **Usage**: Useful for ensuring the note's title is prominently displayed within the note.

### Random Note Retrieval

Insert a link to a random note:

```Templater
<%* let files = app.vault.getMarkdownFiles(); let randomFile = files[Math.floor(Math.random() * files.length)]; tR += `[[${randomFile.path}]]`; %>
```

- **Usage**: Encourages revisiting past notes.

---

## Web Integration Snippets

### Fetching YouTube Video Details

Automatically extract details from a YouTube link in your clipboard:

```Templater
<%* let clipboard = await tp.system.clipboard(); let videoId = clipboard.split('v=')[1]; let apiKey = 'YOUR_YOUTUBE_API_KEY'; let response = await fetch(`https://www.googleapis.com/youtube/v3/videos?id=${videoId}&key=${apiKey}&part=snippet,contentDetails`); let data = await response.json(); let video = data.items[0]; tR += `# ${video.snippet.title}\n\n`; tR += `**Channel**: ${video.snippet.channelTitle}\n`; tR += `**Published**: ${video.snippet.publishedAt}\n`; tR += `**Description**:\n${video.snippet.description}`; %>
```

- **Usage**: Copy a YouTube link, and the template fetches video details.
- **Note**: Replace `YOUR_YOUTUBE_API_KEY` with your actual API key.

### Random Images and Quotes

Insert a random image or quote:

```Templater
![Random Image](https://source.unsplash.com/random/800x600)
> <% await tp.http.get('https://api.quotable.io/random').then(res => JSON.parse(res).content) %>
```

- **Usage**: Enhances notes with inspirational content.

---

## Quick Capture Ideas

Streamline idea capturing without interrupting your workflow:

```Templater
<%* let idea = await tp.system.prompt("Capture your idea:"); let fileContent = `- ${moment().format("HH:mm")}: ${idea}\n`; let filePath = "Quick Capture.md"; await tp.file.append(filePath, fileContent); %>
```

- **Usage**: Triggers a prompt to capture an idea and appends it to `Quick Capture.md`.
- **Tip**: Assign a hotkey for quick access.

---

## Highlight Extraction

Extract all highlighted text from a note:

```Templater
<%* let content = tp.file.content; let highlights = content.match(/==(.+?)==/g); if (highlights) { tR += highlights.map(h => h.replace(/==/g, '')).join('\n\n'); } else { tR += 'No highlights found.'; } %>
```

- **Usage**: Collects all text highlighted using `==highlight==` syntax.

---

## Time with Emojis

Insert the current time with a corresponding clock emoji:

```Templater
<%* let hour = moment().hour(); let emojiHour = hour % 12 || 12; let emoji = `:${emojiHour}oclock:`; tR += `${emoji} ${moment().format('HH:mm')}`; %>
```

- **Example Output**: `🕛 12:46`.

---

## Table of Contents Generation

Generate a table of contents for your note:

```Templater
<%* // Set the maximum header level to include
const maxLevel = await tp.system.prompt("Enter max header level (e.g., 3):", "3");
const content = tp.file.content;
const toc = [];
const regex = new RegExp(`^(#{1,${maxLevel}})\s*(.+)$`, 'gm');
let match;
while ((match = regex.exec(content)) !== null) {
  const level = match[1].length;
  const title = match[2];
  const link = title.toLowerCase().replace(/[^\w]+/g, '-');
  toc.push(`${'  '.repeat(level - 1)}- [${title}](#${link})`);
}
tR += toc.join('\n'); %>
```

- **Usage**: Creates a clickable table of contents based on your headings.

---

## Kindle Clippings Processing

Organize your Kindle highlights:

```Templater
<%* // Ensure 'My Clippings.txt' is in your vault
const file = await app.vault.adapter.read('My Clippings.txt');
const entries = file.split('==========');
for (let entry of entries) {
  // Parse and process each highlight
} %>
```

- **Usage**: Processes the `My Clippings.txt` file and organizes highlights.

---

## Converting Blocks to Callouts

Transform selected text into a callout:

```Templater
<%* // Get the selected text
let selectedText = tp.file.selection();
if (selectedText) {
  tR += `> [!NOTE]\n> ${selectedText}`;
} else {
  tR += 'No text selected.';
} %>
```

- **Usage**: Select text and apply the template to convert it into a callout block.

---

## Adding Timestamps to Frontmatter

Insert file creation and modification dates into the frontmatter:

```Templater
---
created: <% tp.file.creation_date("YYYY-MM-DD HH:mm") %>
modified: <% tp.file.last_modified_date("YYYY-MM-DD HH:mm") %>
---
```

- **Usage**: Helpful for data queries and organization.

---

## Listing Notes Created Today

Generate a list of notes created on the current day:

```Templater
<%* let today = moment().format("YYYY-MM-DD"); let files = app.vault.getMarkdownFiles(); let todayFiles = files.filter(f => moment(f.stat.ctime).format("YYYY-MM-DD") === today); tR += todayFiles.map(f => `- [[${f.path}]]`).join('\n'); %>
```

- **Usage**: Use in your daily note to see all notes created that day.

---

## Additional Resources

- **Moment.js Documentation**: https://momentjs.com/docs/
- **Templater Plugin Guide**: Obsidian Templater Documentation
- **Obsidian Forum**: https://forum.obsidian.md/
- **Community Snippets**: Search the Obsidian Community Discord for shared templates.

---

By incorporating these Templater snippets into your Obsidian workflow, you can automate repetitive tasks, enhance note interconnectivity, and maintain a more organized and efficient note-taking system.

---

_Note_: The code snippets provided are collected from various community sources, including the Obsidian Forum and community articles. Customize the snippets to fit your specific workflow and directory structure.

[[Obsidian]]   [[Obsidian Templater Guide]]
