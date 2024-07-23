| Command       | Effect                                                         |
| ------------- | -------------------------------------------------------------- |
| :jumps        | shows a list of possible jumps                                 |
| `<C-o>`       | like a back button for jumps                                   |
| `<C-i>`       | like a forward button for jumps                                |
| [count]G      | jump to line number                                            |
| /pattern      | jump to next pattern                                           |
| %             | jump to matching parenthesis                                   |
| (/)           | jump to start of previous or next sentence                     |
| {/}           | jump to start of previous or next paragraph                    |
| H / M / L     | jump to top/ middle/ bottom of file                            |
| gf            | jump to file name under the cursor                             |
| `<C-]>`       | jump to definition of keyword under the cursor                 |
| `mark / 'mark | jump to a mark                                                 |
| g;            | move cursor to the previous change same as doing `u<C-r>`      |
| g,            | move cursor to the next change                                 |
| gi            | go to the last place you inserted text and go into insert mode |
apart from the first three rows of this table all of these are treated as motions and so are stored in :jumps 