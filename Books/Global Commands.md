`:[range] global[!] /{pattern}/ [cmd]`
default range is entire file (%)
- `:vglobal` does the inverse and runs the command on all lines that do not match
- you can use `:g` and `:v` as abbreviations

## Deleting lines containing patterns
see [[Pattern Matching]]
### Example - delete all lines with tags
- get pattern `/\v\<\/?\w+>`
- run `:g//d`
### Example - delete all lines that aren't href
- `:v/href/d`

## Yanking 
### Example - showing TODOs
- `:g/TODO` will print all todos
- to yank all todos into a register run the following:
	- clear a register `qaq`
	- run `:g/TODO/yank A`
	- `reg a` will show all the TODOs, you could also paste these
- paste all todos at the end of the page with `:g/TODO/t$` for t see [[Command Mode]]
see [[Registers]]
