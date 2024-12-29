---
aliases:
  - Machine Learning
---

[Unit Page](https://uob-coms30035.github.io/)
# Lessons
```dataview
TABLE without ID file.link as Title
From "Uni Modules/Machine Learning"
Where file != this.file and contains(file.tags, "#Lesson")
```

# All Notes
```dataview
TABLE without ID file.link as Title,  filter(file.tags, (t) => t != "#Lesson") as "Tags"
From "Uni Modules/Machine Learning"
Where file != this.file
```
