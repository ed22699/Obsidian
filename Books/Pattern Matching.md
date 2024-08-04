| Pattern | Effect                                                                                                         |
| ------- | -------------------------------------------------------------------------------------------------------------- |
| \c      | search but ignore case                                                                                         |
| \C      | search do not ignore case                                                                                      |
| \v      | enables very magic search where regex acts more like it does in python                                         |
| \V      | turns off all regular expressions so a.k.a will only search for that rather than seeing the . as any character |
| \zs     | start of a match                                                                                               |
| \ze     | end of a match                                                                                                 |
### regular expression shortcuts
`\x` = `[0-9a-fA-F]`
- this means `/\v#(\x{6}|\x{3})` can be used to find hex values
- `/\v<(\w+)\_s+\1>` matches duplicate words
	- `\1` refers to the first pattern within (), this goes up to 9 with 0 being the entire match (adding `%` in front of the brackets will stop it from being assigned `\1`)
	- `<` and `>` match word boundaries this means searching for the wont also find there
	- `\_s` matches whitespace or line break

| Expressions | Meaning                             |
| ----------- | ----------------------------------- |
| `\1`        | first pattern within ()             |
| `\_s`       | whitespace or line break            |
| `.`         | single character                    |
| `+`         | as many characters                  |
| `[^']+`     | as many characters that are not '   |
| `\w`        | word                                |
| `\W`        | WORD                                |
| `\|`        | choice (note the \ is not included) |
`q/` can be used to bring up the history (see [[Command Mode]])
### Boundaries of a match example
| Keystrokes             | Buffer Contents                                                      |
| ---------------------- | -------------------------------------------------------------------- |
| {start}                | Match "quoted words" ---not quote marks                              |
| `/\v"[^"]+"<CR>`       | Match "quoted words" ---not quote marks ("quoted words" highlighted) |
| `/\v"\zs[^"]+\ze"<CR>` | Match "quoted words" ---not quote marks (quoted words highlighted)   |

- use the `?` for phrases with lots of problem characters as a back search and `/` for individual problem characters 
- to paste the entire problem hyperlink into the search start the search with `/<C-r>=` and then enter `escape(@u, getcmdtype().'\'` and then enter
## Searching - related to [[Normal Mode]]
| Command      | Effect                                                                                                               |
| ------------ | -------------------------------------------------------------------------------------------------------------------- |
| gn           | search in visual mode forward                                                                                        |
| gN           | search in visual mode backward                                                                                       |
| `<C-r><C-w>` | paste the remainder of the highlighted word into the search (note will paste whole word instead if `\v` is involved) |
| `/e`         | position cursor on the end of the search term                                                                        |
>[!NOTE]
> the use of `//` will use the last search term

## Counting matches
### Via substitution
`:%s///gn`
5 matches on 4 lines
### Via :vimgrep
`:vimgrep //g %` (% keeps it to the current buffer)
(3 of 5): viewport.buttons.previous.show();
use `cnext` and `cprev` to traverse

## Sort CSS 
- select the area `vi{`
- run `:'<,'>sort`
alternatively you can run 
- `:g/{/ .+1,/}/-1 sort`