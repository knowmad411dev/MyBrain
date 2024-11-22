<%* let videoUrl = await tp.system.prompt("Enter YouTube video URL"); 
let metadata = await tp.user.ytmeta(`-j "${videoUrl}"`, "."); 
let title = metadata.title; 
let description = metadata.description; 
let duration = metadata.duration; 
let chapters = metadata.chapters;
-%> 
# [[<% title %>]] 

URL:  <% videoUrl %> 
Duration:  <% duration %> 
## Description 
<% description %> 

## Chapters 
<%* if (chapters) { -%> <% chapters.map(ch => `- [${ch.title}](${videoUrl}&t=${ch.start_time}) (${ch.start_time})`).join('\n') %> <%* } -%> 

## Notes