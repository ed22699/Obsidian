A way of indexing files so that you can jump to definitions. This can also be done with an lsp instead. 
- create file with `ctags *.rb`
if in vim:
- set tags with `:set tags?`
- create file with `:!ctags -R`
- use `<C-]>` to jump to and `<C-t>` to go back