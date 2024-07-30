- When a macro fails it will abort, this can be a good fail safe and sometimes we will want this and so should run the macro in series like so
```markdown
1. First item
2. Second item
3. third item
not an item
do not edit these lines
```
If we wanted to edit all the list items to be 1) form instead we could run `20@{register}` and this will stop when it hits the fail safe, in this case the `f.` will fail and so the last two lines will not be affected
- Sometimes we do not want this affect and instead should run more in parallel
```markdown
1. First item
2. Second item
3. third item
not an item
4. forth item
5. fifth item
```
Here you would want to edit all the items in the list, doing it in series it would stop on the 4th line. However if you select it all in visual mode and then run `:'<,'>normal @{register}` this will reformat all the list items
see [[Command Mode]]

| Command | Effect                         |
| ------- | ------------------------------ |
| :reg a  | shows the macro in that reg    |
| qa      | record macro to a              |
| qA      | append onto the end of macro a |
|         |                                |
## Run macro across files - see [[Files]]
### Parallel 
- first create the list of arguments `:args *.rb`
- record the macro (do not save file)
- run `:edit!` to reverse changes to the file
- run `:argdo normal @a` to run on all files
### Series
- edit the macro to go to next file `:next`
- run `22@a` this will run across buffers until and issue is found
>[!NOTE] 
>When running macros across files try do it in series so errors are not missed

## Run macro with vim script
| Keystrokes            | Buffer Contents                                                                                             |
| --------------------- | ----------------------------------------------------------------------------------------------------------- |
| `:let i=1`            | partridge in a pear tree                                                                                    |
| `qa`                  | partridge in a pear tree                                                                                    |
| `I<C-r>=i<CR>) <Esc>` | 1) partridge in a pear tree                                                                                 |
| `:let i+=1`           | 1) partridge in a pear tree                                                                                 |
| `q`                   | 1) partridge in a pear tree                                                                                 |
| `jVG`                 | 1) partridge in a pear tree<br>turtle doves<br>French hens<br>calling birds<br>golden rings                 |
| `:'<,'>normal @a`     | 1) partridge in a pear tree<br>2) turtle doves<br>3) French hens<br>4) calling birds<br>5) golden rings<br> |
## Editing a macro
1. record the macro e.g to register a
2. `:put a` to enter the macro into the next line
3. make changes to that line 
4. yank to end of line back into register a, this will complete the change
>[!NOTE]
>it is better to use `"ay$` over `"ayy` as yanking the whole line will add `^J` to the end
