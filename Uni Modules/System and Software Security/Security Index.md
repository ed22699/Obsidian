---
aliases:
  - System and Software Security
tags:
  - index
---

[Unit Page](https://cs-uob.github.io/COMSM0049/)
- Youtube man LiveOverflow
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