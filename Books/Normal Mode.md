
| Command      | Effect                                                                 |
| ------------ | ---------------------------------------------------------------------- |
| >G           | indents                                                                |
| .            | Repeat last command, also works for all keystrokes done in insert mode |
| ;            | Repeat last search command (f or n)                                    |
| ,            | Reverse of ;                                                           |
| *            | Executes a search of the word under the cursor                         |
| `<C-a>`      | increments the next number on the line                                 |
| `<C-x>`      | decrements the next number on the line                                 |
| g            | a prefix that modifies the behaviour of the subsequent keystroke       |
| ga           | get the hex and decimal number for the symbol                          |
| gv           | reselects the last visual mode selection                               |
| K            | looks up documentation for what is under the cursor                    |
| J            | joins the line below                                                   |
| :read !{cmd} | will print the output of the shell command under where the cursor is   |

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

using shell can be very powerful, give a range before it and it will take the lines of that range as input meaning you can do stuff like this
`:2,$ !sort -t ',' -k2`
if you use !G it will put :.,$! into the Ex command automatically
see [[Command Mode]]

## Detailed Branches
- [[Jumps]]
- [[Files]]
- [[Marks]]
- [[Registers]]
- [[Macros]]
- [[Spell Checker]]
- [[ctags]]