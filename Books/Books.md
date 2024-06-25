```dataview
TABLE WITHOUT ID file.link AS "Title", author as Author, ("![coverimg|100](" + coverUrl + ")") as Cover, 
Status, totalPage as "Pages"
From "Books"
WHERE file != this.file
```