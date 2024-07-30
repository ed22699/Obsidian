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

### Boundaries of a match example
| Keystrokes             | Buffer Contents                                                      |
| ---------------------- | -------------------------------------------------------------------- |
| {start}                | Match "quoted words" ---not quote marks                              |
| `/\v"[^"]+"<CR>`       | Match "quoted words" ---not quote marks ("quoted words" highlighted) |
| `/\v"\zs[^"]+\ze"<CR>` | Match "quoted words" ---not quote marks (quoted words highlighted)   |

- use the `?` for phrases with lots of problem characters as a back search and `/` for individual problem characters 
- 