[Unit Page](https://uob-coms30035.github.io/)
# Lessons
```dataview
TABLE without ID file.link as Title
From "Uni Modules/Image Processing and Computer Vision"
Where file != this.file and contains(file.tags, "#Lesson")
```

# All Notes
```dataview
TABLE without ID file.link as Title,  filter(file.tags, (t) => t != "#Lesson") as "Tags"
From "Uni Modules/Image Processing and Computer Vision"
Where file != this.file
```
