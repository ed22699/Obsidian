| Command | Effect                                                                 |
| ------- | ---------------------------------------------------------------------- |
| >G      | indents                                                                |
| .       | Repeat last command, also works for all keystrokes done in insert mode |
| ;       | Repeat last search command (f or n)                                    |
| ,       | Reverse of ;                                                           |
| *       | Executes a search of the word under the cursor                         |
| `<C-a>` | increments the next number on the line                                 |
| `<C-x>` | decrements the next number on the line                                 |
| g       | a prefix that modifies the behaviour of the subsequent keystroke       |

Operator + Motion = Action

| Operators | Effect                                            |
| --------- | ------------------------------------------------- |
| c         | Change                                            |
| d         | Delete                                            |
| y         | Yank into register                                |
| gu        | Make lowercase                                    |
| gU        | Make uppercase                                    |
| >         | Shift right                                       |
| <         | Shift left                                        |
| =         | Autoindent                                        |
| !         | Filter {motion} lines through an external program |
