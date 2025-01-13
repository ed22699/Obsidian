---
tags:
  - favorite
---

# Lessons
```dataview
TABLE without ID file.link as Title
From "Uni Modules/Data Science"
Where file != this.file and contains(file.tags, "#Lesson")
```
# All Notes
```dataview
TABLE without ID file.link as Title,  filter(file.tags, (t) => t != "#Lesson") as "Tags"
From "Uni Modules/Data Science"
Where file != this.file
```
