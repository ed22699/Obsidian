| Command               | Effect                            | Repeat | Reverse |
| --------------------- | --------------------------------- | ------ | ------- |
| /pattern              | search for that pattern forwards  | n      | N       |
| ?pattern              | search for that pattern backwards | n      | N       |
| :s/target/replacement | substitution                      | &      | u       |
|                       |                                   |        |         |


| Command                         | Effect                                                            |
| ------------------------------- | ----------------------------------------------------------------- |
| :[range]delete[x]               | Delete specified lines [into register x]                          |
| :[range]yank [x]                | Yank specified lines [into register x]                            |
| :[line]put [x]                  | Put the text from register x after the specified line             |
| :[range]copy {address}          | Copy the specified lines to below the line specified by {address} |
| :[range]move {address}          | Move the specified lines to below the line specified by {address} |
| :[range]join                    | Join the specified lines                                          |
| :[range]normal {commands}       | Execute Normal mode {commands} on each specified line             |
| :[range]substitute/{pattern}/{} |                                                                   |
