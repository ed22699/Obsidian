---
aliases:
  - Internet Economics and Financial Technology
tags:
  - favorite
  - index
---

[Unit Page]()
# Lessons
```dataview
TABLE without ID file.link as Title
From "Uni Modules/Internet Economics and Financial Technology"
Where file != this.file and contains(file.tags, "#Lesson")
```

# All Notes
```dataview
TABLE without ID file.link as Title,  filter(file.tags, (t) => t != "#Lesson") as "Tags"
From "Uni Modules/Internet Economics and Financial Technology"
Where file != this.file
```