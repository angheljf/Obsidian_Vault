<%*
  let title = tp.file.title
  if (title.startsWith("Untitled")) {
    title = await tp.system.prompt("Title");
    await tp.file.rename(title);
  } 
  
  tR += "---"
%>
title: <%* tR += title %>
created: <% tp.date.now("YYYY-MM-DD H:m") %>
last modified: <% tp.file.last_modified_date("YYYY-MM-DD H:m") %>
aliases: 
tags: AI, UL
type:
---
Notes

---
>Related Notes: 
>Tags: 
