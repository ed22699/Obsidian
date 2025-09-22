---
aliases:
  - Design Verification
tags:
  - index
---

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

link back to **observability** and **controlability** when answering questions




book points
- just because it is proven correct does not mean it will do what you intend 
- there are limits to what can be proven
- Complexity, with very large systems it is unsure whether it will work just because it works on the smaller scale
- human interaction, you can not be sure that the system will be used in the exact way intended
- many levels of correctness, correct at one level does not mean correctness everywhere. In order for a system to be reliable it has to be correct at every relevant level (we don't know what the relevant levels are)
- models are inherently abstract and so special cases will be missed, if they were not abstract the system would be too sensitive