## Read / Reading List
```dataview
TABLE WITHOUT ID file.link AS "Title", 
Status
From #Blog
WHERE file != this.file and status != null and status != "To Read"
```
## To Read List
```dataview
TABLE WITHOUT ID file.link AS "Title", 
Status
From #Blog
WHERE file != this.file and status = "To Read"
```