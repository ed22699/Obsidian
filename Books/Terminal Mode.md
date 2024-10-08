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
- `p` pastes to the command cursor position
- when cursor is on file path you can use `gf` to open that file
- use `nvr` over `nvim` when in neovims terminal emulator

| Command          | Effect                              |
| ---------------- | ----------------------------------- |
| `nvr <file>`     | open file in the current window     |
| `nvr -\| <file>` | open file in the last active window |
| `nvr -o <file>`  | open file or files via `:split`     |
| `nvr -O <file>`  | open file of files via `:vsplit`    |
| `nvr -p <file>`  | open file or files via `:tabedit`   |
note p86
- `<C-x><C-e>` to edit a terminal command in neovim