---
aliases:
  - System and Software Security
tags:
  - favorite
  - index
---

[Unit Page]()
# Lessons
```dataview
TABLE without ID file.link as Title
From "Uni Modules/System and Software Security"
Where file != this.file and contains(file.tags, "#Lesson")
```

# All Notes
```dataview
TABLE without ID file.link as Title,  filter(file.tags, (t) => t != "#Lesson") as "Tags"
From "Uni Modules/System and Software Security"
Where file != this.file
```