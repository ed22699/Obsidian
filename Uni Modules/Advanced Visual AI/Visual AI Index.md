---
aliases:
  - Advanced Visual AI
tags:
  - index
---

[Unit Page]()
# Lessons
```dataview
TABLE without ID file.link as Title
From "Uni Modules/Advanced Visual AI"
Where file != this.file and contains(file.tags, "#Lesson")
```

# All Notes
```dataview
TABLE without ID file.link as Title,  filter(file.tags, (t) => t != "#Lesson") as "Tags"
From "Uni Modules/Advanced Visual AI"
Where file != this.file
```