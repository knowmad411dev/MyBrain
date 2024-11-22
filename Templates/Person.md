---
alias: 
tags: [person]
birthdate: <% tp.prompt("Enter birthdate (YYYY-MM-DD):") %>
status: <% tp.prompt("Status (active/inactive):") %>
---

# <% tp.file.title %>

## Basic Information
- **Full Name:** <% tp.prompt("Enter full name:") %>
- **Nickname:** <% tp.prompt("Enter nickname (if any):") %>
- **Gender:** <% tp.prompt("Enter gender:") %>
- **Place of Birth:** <% tp.prompt("Enter place of birth:") %>

## Professional Information
- **Occupation:** <% tp.prompt("Enter occupation:") %>
- **Company/Organization:** [[<% tp.prompt("Enter company/organization:") %>]]

## Relationships
- **Spouse/Partner:** [[<% tp.prompt("Enter spouse/partner:") %>]]
- **Children:** [[<% tp.prompt("Enter children (comma-separated):") %>]]
- **Friends:** [[<% tp.prompt("Enter friends (comma-separated):") %>]]

##  Notes
- **First Met:** <% tp.date.now("YYYY-MM-DD") %>
- **Notable Moments:** <% tp.prompt("Enter notable moments (optional):") %>
- **Future Plans:** <% tp.prompt("Enter future plans/topics (optional):") %>

---

### Usage Instructions:
1. **Save the Template** in your `Templates` folder as `Person Template.md`.
2. Use the Templater command to insert it into a new note.

---

This version captures the essentials with minimal fields. You can always expand later by adding more sections as needed.
