## Read / Reading List
```dataview
TABLE WITHOUT ID file.link AS "Title", author as Author, ("![coverimg|100](" + coverUrl + ")") as Cover, 
Status, totalPage as "Pages"
From #Book
WHERE file != this.file and status != null and status != "To Read"
```
## To Read List
```dataview
TABLE WITHOUT ID file.link AS "Title", author as Author, ("![coverimg|100](" + coverUrl + ")") as Cover, 
Status, totalPage as "Pages"
From #Book
WHERE file != this.file and status = "To Read"
```