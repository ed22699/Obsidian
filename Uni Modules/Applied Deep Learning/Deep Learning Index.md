---
aliases:
  - Applied Deep Learning
tags:
  - index
---

[Unit Page](https://comsm0045-applied-deep-learning.github.io/)
# Lessons
```dataview
TABLE without ID file.link as Title
From "Uni Modules/Applied Deep Learning"
Where file != this.file and contains(file.tags, "#Lesson")
```

# All Notes
```dataview
TABLE without ID file.link as Title,  filter(file.tags, (t) => t != "#Lesson") as "Tags"
From "Uni Modules/Applied Deep Learning"
Where file != this.file
```