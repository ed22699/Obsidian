
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