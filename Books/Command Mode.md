| Command               | Effect                            | Repeat | Reverse |
| --------------------- | --------------------------------- | ------ | ------- |
| /pattern              | search for that pattern forwards  | n      | N       |
| ?pattern              | search for that pattern backwards | n      | N       |
| :s/target/replacement | substitution                      | &      | u       |
|                       |                                   |        |         |


| Command                                       | Effect                                                                                                                      |
| --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| :[range]delete[x]                             | Delete specified lines [into register x]                                                                                    |
| :[range]yank [x]                              | Yank specified lines [into register x]                                                                                      |
| :[line]put [x]                                | Put the text from register x after the specified line                                                                       |
| :[range]copy {address}                        | Copy the specified lines to below the line specified by {address}                                                           |
| :[range]move {address}                        | Move the specified lines to below the line specified by {address}                                                           |
| :[range]join                                  | Join the specified lines                                                                                                    |
| :[range]normal {commands}                     | Execute Normal mode {commands} on each specified line (can use norm)                                                        |
| :[range]substitute/{pattern}/{string}/[flags] | Replace occurrences of {patter} with {string} on each specified line                                                        |
| :[range]global/{pattern}/[cmd]                | Execute the Ex command [cmd] on all specified lines where the {pattern} matches                                             |
| :[range]t{address}                            | same as copy                                                                                                                |
| :[range]m{address}                            | same as move                                                                                                                |
| @:                                            | repeat last Ex                                                                                                              |
| `<C-d>`                                       | show list of possible completions                                                                                           |
| `<tab>`                                       | autocomplete                                                                                                                |
| :%s//change/g                                 | change all of the last searched word to change (subsitution)                                                                |
| `<C-r><C-w>`                                  | copy the word where the cursor is and paste it into command area (`<C-a>` if you want to paste the equivalent of W instead) |
| :!{shell command}                             | runs the shell command without leaving vim                                                                                  |
| :source {shell script name.vim}               | runs the series of vim commands                                                                                             |
| :argdo source batch.vim                       | run the script in all launched files (launch multiple with `*.html` for example)                                            |
before executing a normal command vim moves the cursor to the start of the line
if you use q: you can enter command-line window and alter then run commands

| command | action                                                  |
| ------- | ------------------------------------------------------- |
| q/      | open the command-line window with history of searches   |
| q:      | open the command-line window with history of Ex command |
| `<C-f>` | switch from command-line mode to command line window    |

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
