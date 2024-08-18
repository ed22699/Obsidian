| Command       | Effect                                                                |
| ------------- | --------------------------------------------------------------------- |
| `:mksession!` | saves a session                                                       |
| `nvim -S`     | runs previous session `:source Session.vim` produces the same results |
|               |                                                                       |
- session records the buffer list, buffer names, windows, tab pages
- if you name a terminal session through `:te {cmd}` when reopening the command will be ran, however if it was named `:te` a default shell will take the place
- you can rename the file using `:file term://{cmd}` and so this command will be ran upon initiation [[Terminal Mode]]