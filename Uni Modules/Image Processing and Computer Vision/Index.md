[Unit Page](https://www.ole.bris.ac.uk/webapps/blackboard/content/listContent.jsp?course_id=_260097_1&content_id=_8655934_1&mode=reset)
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

## Questions

1. what is the use of Dirac delta-function (spatial brightness pulse)
![[Dirac Delta-Function]]

