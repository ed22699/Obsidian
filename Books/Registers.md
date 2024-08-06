| Command   | Effect                          |
| --------- | ------------------------------- |
| "add      | deleted and store in register a |
| "app      | paste from register a           |
| :delete c | delete and store in register c  |
| :put c    | put from register c             |
- Unlike they unnamed register the yank register (0) persists until the next yank, unaffected by c, x and d
- "_ is the black hole register, nothing is saves that is stored here, this is useful if you don't want to overwrite the unnamed register
- "+ is the system clipboard register, use this to copy and paste to and from external applications
- "= is the expression register, it takes you to command line mode where you can write a script. If it outputs a string it will be used
- "" is the unnamed register

## Read only registers

| Register | Contents                   |
| -------- | -------------------------- |
| "%       | name of the current file   |
| "#       | name of the alternate file |
| ".       | last inserted test         |
| ":       | last Ex command            |
| "/       | last search pattern        |
