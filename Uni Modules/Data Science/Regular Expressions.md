---
tags:
  - web_scraping
---
- sequences of characters that define a search pattern
- in Python there are two main options for executing regular expression:
	- `re.match`
	- `re.search`
```python
# attempts to match the RE pattern to the start of the string
re.match(pattern, stringm, flags=0)

# attempts to match the RE pattern to any point in the string
re.search(pattern, string, flags=0)
```
- [Cheat sheet](https://www.dataquest.io/wp-content/uploads/2019/03/python-regular-expressions-cheat-sheet.pdf)
```python
import re

line = "Cats are smarter than dogs"
matchObj = re.match(r"(.*) are (.*?) than (.*)", line, re.I)

print("matchObj.group()", matchObj.group())
# "Cats are smarter than dogs"

print("matchObj.group(1)", matchObj.group(1))
# "Cats"

print("matchObj.group(2)", matchObj.group(2))
# "smarter"

print("matchObj.group(3)", matchObj.group(3))
# "dogs"
```