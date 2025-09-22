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
```c
if (access("/tmp/X", W_OK)) { 
	f = open("/tmp/X");
	write_to_file(f); 
} else { 
	printf("Nope.\n"); 
}
```
- what happens if we swap out the temporary file with a link to a file we wouldn't normally have access to after the access control check is done, but before the open has started
	- can use a command like `ln -s /etc/password /tmp/X`
### Assumption
- assumption is that nothing can happen between check and use of data; but this assumption isn't always right
	- be really careful when splitting things into steps
	- some static analysis tools can spot things