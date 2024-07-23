Use to save a cursor position so you can jump back to it
using capital letters for marks create global marks which can be entered from other files

| Command   | Effect                                        |
| --------- | --------------------------------------------- |
| m{a-zA-Z} | mark to that postion                          |
| `{a-zA-Z} | jump to that postion                          |
| '{a-zA-Z} | jump to that line                             |
| ``        | position before last jump within current file |
| `.        | location of last change                       |
| `^        | location of last insertion                    |
| `[        | Start of last change or yank                  |
| `]        | End of last change or yank                    |
| `<        | Start of last visual selection                |
| `>        | End of last visual selection                  |
