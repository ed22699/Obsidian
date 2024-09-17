[Unit Page](https://uobdv.github.io/Design-Verification/)
# Lessons
```dataview
TABLE without ID file.link as Title
From "Uni Modules/Design Verification"
Where file != this.file and contains(file.tags, "#Lesson")
```

# All Notes
```dataview
TABLE without ID file.link as Title,  filter(file.tags, (t) => t != "#Lesson") as "Tags"
From "Uni Modules/Design Verification"
Where file != this.file
```
