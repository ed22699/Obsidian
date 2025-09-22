---
tags:
  - interesting_bugs
---
- computers can do more than one thing at once and the order is important
- what happens if $n$ is dereferenced again before the increment function has had time to complete
	- we will lose one or more of the increments
	- well understood correctness issue
	- fix by implementing synchronous blocks or locking
### Access and Open
- assumption is that nothing can happen between check and use of data; but this assumption isn't always right
	- be really careful when splitting things into steps
	- some static analysis tools can spot things