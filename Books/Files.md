
## Buffers

| Command           | Effect                                                                                    |
| ----------------- | ----------------------------------------------------------------------------------------- |
| :bnext            | goes to next buffer                                                                       |
| :ls               | lists the buffers                                                                         |
| `<C-^>`           | toggle between last two files                                                             |
| :bprev            | goes to previous buffer                                                                   |
| :bfirst           | goes to first                                                                             |
| :blast            | goes to last                                                                              |
| :buffer [number]  | goes to the buffer with that number (can also use enough letters to make the name unique) |
| :bufdo            | execute command in all buffers listed                                                     |
| :bdelete N1 N2 N3 | delete specified buffers can use :bd for short                                            |
| :N,M bdelete      | delete buffers in that range                                                              |
vim creates a new buffer everytime we open a new file
- group buffers into a collection with the argument list
	- buffers are quite inflexible so it isn't worth deleting them as you go along, use argument lists instead to group

## Arguments
| Command                 | Effect                                                                                      |
| ----------------------- | ------------------------------------------------------------------------------------------- |
| :args                   | argument list                                                                               |
| :args {arglist}         | change the arg list this can be with filenames, wildcards or shell commands                 |
| :args `**/*.*`          | get all files in that directory or subdirectories and put as arguments                      |
| :args ``cat .chapters`` | note this has the comma things on it. Adds all the files from each line of chapters to args |
** is like * however it recurses it search downward into directories below the specified directory
## Windows
| Command          | Effect                                          |
| ---------------- | ----------------------------------------------- |
| `<C-w>s`         | split horizontally                              |
| `<C-w>v`         | split vertically                                |
| :sp[lit] {file}  | split horizontally loading file into new window |
| :vsp[lit] {file} | split vertically loading file into new window   |
| :clo[se]         | close the active window `<C-w>c`                |
| :on[ly]          | keep only the active window `<C-w>o`            |
| `<C-w>=`         | lize width and height of all windows            |
| `<C-w>_`         | Maximize height of active window                |
| `<C-w>\|`        | Maximize width of active window                 |
| `[N]<C-w>_`      | set the height to [N] rows                      |
| `[N]<C-w>\|`     | set the width to [N] columns                    |
| `<C-w>H`         | move current window to far left                 |
| `<C-w>J`         | move current window to bottom                   |
| `<C-w>K`         | move current window to top                      |
| `<C-w>L`         | move current window to far right                |
## Tabs
Vim's tab pages are not mapped to buffers in a one-to-one relationship. Instead it is a container that can hold a collection of windows

| Command     | Effect                                       |
| ----------- | -------------------------------------------- |
| `<C-w>T`    | move the current window to its own tab       |
| :tabc[lose] | close the current tab and all its windows    |
| :tabo[nly]  | keep the active tab page, closing all others |
| {N}gt       | switch to tab page number {N}                |
| gt          | switch to the next tab                       |
| gT          | switch to the previous tab                   |
