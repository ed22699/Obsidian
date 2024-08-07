| Command | Effect                                       |
| ------- | -------------------------------------------- |
| `]s`    | Jump to next spelling error                  |
| `[s`    | Jump to previous spelling error              |
| `z=`    | Suggest corrections for current word         |
| `zg`    | Add current word to spell file               |
| `zw`    | Remove current word from spell file          |
| `zug`   | Revert `zg` or `zw` command for current word |
`:let spelllang="en_gb"` sets the spelling to just British english
- you can set multiple spell files via `setlocal spellfile=~/.vim/spell/en.utf-8.add` and `setlocal spellfile+=~/books/practical_vim/jargon.utf-8.add` with this we can have special vim terminology in our jargon file
	- with this you can now add terminology to `en.utf-8` with `1zg` or add to `jargon.utf-8` with `2zg`

## Autocorrect in insert mode
`<C-x><C-s>` and `<C-x>s` both work
- this is useful when you have multiple errors on a line