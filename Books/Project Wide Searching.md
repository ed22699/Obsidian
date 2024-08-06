`:grep Waldo *` will search all files in the current directory for Waldo - `-i` makes it case insensitive 
- you can navigate through these files and positions the same way you do with compilers, using `:cnext/:cprev`
`vim[grep] /going/g clock.txt tough.txt where.txt` will find all the occurrences of going in those three files `:vim[grep][!] /{pattern}/[g][j] {file} ...`
- you can use ## to represent the names of each file in the argument list:
	- `:args *.txt`
	- `:vim /going/g ##`

