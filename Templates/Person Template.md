---
alias: null
birthdate: <% tp.prompt("Enter birthdate (YYYY-MM-DD):") %>
status: <% tp.prompt("Status (active/inactive):") %>
tags:
- templater
---

# <% tp.file.title %>

## Basic Information
- **Full Name:** <% tp.prompt("Enter full name:") %>
- **Nickname:** <% tp.prompt("Enter nickname (if any):") %>
- **Gender:** <% tp.prompt("Enter gender:") %>
- **Place of Birth:** <% tp.prompt("Enter place of birth:") %>

## Professional Information
- **Occupation:** <% tp.prompt("Enter occupation:") %>
<%*
let company = await tp.prompt("Enter company/organization:");
if (company) await tp.file.create_new(company, "# " + company);
%>
- **Company/Organization:** [[<% company || "Unknown Company" %>]]

## Relationships
<%*
let spouse = await tp.prompt("Enter spouse/partner:");
if (spouse) await tp.file.create_new(spouse, "# " + spouse);
%>
- **Spouse/Partner:** [[<% spouse || "No Spouse/Partner" %>]]

<%*
let children = await tp.prompt("Enter children (comma-separated):");
if (children) {
    let childrenArray = children.split(",").map(child => child.trim());
    for (let child of childrenArray) {
        await tp.file.create_new(child, "# " + child);
    }
}
%>
- **Children:** <% children ? children.split(",").map(child => `[[${child.trim()}]]`).join(", ") : "No Children" %>

<%*
let friends = await tp.prompt("Enter friends (comma-separated):");
if (friends) {
    let friendsArray = friends.split(",").map(friend => friend.trim());
    for (let friend of friendsArray) {
        await tp.file.create_new(friend, "# " + friend);
    }
}
%>
- **Friends:** <% friends ? friends.split(",").map(friend => `[[${friend.trim()}]]`).join(", ") : "No Friends" %>

## Notes
- **First Met:** <% tp.date.now("YYYY-MM-DD") %>
- **Notable Moments:** <% tp.prompt("Enter notable moments (optional):") %>
- **Future Plans:** <% tp.prompt("Enter future plans/topics (optional):") %>
