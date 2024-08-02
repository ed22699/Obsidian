uses [[Pattern Matching]]
`:[range]s[ubstitution]/{pattern}/{string}/[flags]`
for range examples see [[Command Mode]]

| flag | effect                                                                 |
| ---- | ---------------------------------------------------------------------- |
| g    | implement globally, this means all instances on a line will be changed |
| n    | the number of changes that would occur on that substitution            |
| c    | gives you the opputuinity to confirm each change                       |
| &    | reuse same flags as last substitution                                  |

## Special characters 
| Symbol           | Effect                                                           |
| ---------------- | ---------------------------------------------------------------- |
| `\r`             | insert a carriage return                                         |
| `\t`             | insert a tab c ha rac ter                                        |
| `\\`             | insert single backslash                                          |
| `\1`             | insert first submatch                                            |
| `&`              | insert entire matched pattern                                    |
| `~`              | use string from the previous invocation of substitute            |
| `\={vim script}` | evaluate vim script expression; use result as replacement string |
If you think you'll reuse the substitution rather than doing `//` to use previous pattern fill it in explicitly with `/<C-r>//`

`:%s//\=@0/g` replaces the last pattern with what is in the yank register
to create a pretty generic reusable command we can run
```vim
:let @/='Pragmatic Vim'
:let @a='Practical Vim'
:%s//\=@a/g
```
We can then use the substitute command multiple times, changing the register `/` and `a` where suitable 

if you want to reuse a previous command to change it slightly you can run `:%s//~/&`, however if you want to rerun the exact command on the whole file you can simply type `g&`