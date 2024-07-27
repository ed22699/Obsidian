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

| Command | Effect                         |
| ------- | ------------------------------ |
| :reg a  | shows the macro in that reg    |
| qa      | record macro to a              |
| qA      | append onto the end of macro a |
|         |                                |
