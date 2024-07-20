| Command               | Effect                            | Repeat | Reverse |
| --------------------- | --------------------------------- | ------ | ------- |
| /pattern              | search for that pattern forwards  | n      | N       |
| ?pattern              | search for that pattern backwards | n      | N       |
| :s/target/replacement | substitution                      | &      | u       |
|                       |                                   |        |         |


| Command                                       | Effect                                                                          |
| --------------------------------------------- | ------------------------------------------------------------------------------- |
| :[range]delete[x]                             | Delete specified lines [into register x]                                        |
| :[range]yank [x]                              | Yank specified lines [into register x]                                          |
| :[line]put [x]                                | Put the text from register x after the specified line                           |
| :[range]copy {address}                        | Copy the specified lines to below the line specified by {address}               |
| :[range]move {address}                        | Move the specified lines to below the line specified by {address}               |
| :[range]join                                  | Join the specified lines                                                        |
| :[range]normal {commands}                     | Execute Normal mode {commands} on each specified line                           |
| :[range]substitute/{pattern}/{string}/[flags] | Replace occurrences of {patter} with {string} on each specified line            |
| :[range]global/{pattern}/[cmd]                | Execute the Ex command [cmd] on all specified lines where the {pattern} matches |
| :[range]t{address}                            | same as copy                                                                    |
| :[range]m{address}                            | same as move                                                                    |
| @:                                            | repeat last Ex                                                                  |
before executing a normal command vim moves the cursor to the start of the line

| Symbol | Address                                       |
| ------ | --------------------------------------------- |
| $      | the last line of the file                     |
| %      | the whole file                                |
| 1      | first line of the file                        |
| 0      | virtual line above the first line of the file |
| .      | line where the cursor is placed               |
| 'm     | line containing the mark m                    |
| '<     | start of visual section                       |
| '>     | end of visual section                         |
