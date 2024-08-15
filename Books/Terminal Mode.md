| Command                      | Effect                                                   |
| ---------------------------- | -------------------------------------------------------- |
| `i, I, a, A`                 | switch to terminal mode                                  |
| `<C-^>`                      | cycle between the two most recent buffers. See [[Files]] |
| `:[num]bwipeout`             | terminates the buffer of that number                     |
| `:terminal {cmd}`            | terminal buffer is created in the current window         |
| `:split \| terminal {cmd}`   | terminal buffer is created in a horizontal split         |
| `:vsplit \| terminal {cmd}`  | terminal buffer is created in a vertical split           |
| `:tabedit \| terminal {cmd}` | terminal buffer is created in a new tab page             |
- You can run terminal commands that activate the shell by substituting the `!` for `terminal` in command mode