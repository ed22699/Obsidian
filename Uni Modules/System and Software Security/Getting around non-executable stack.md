---
tags:
  - Article
---
[Bugtraq: Getting around non-executable stack (and fix)](https://seclists.org/bugtraq/1997/Aug/63)

- fix
	- change address shared libraries `mmap()` in such a way so it always contains a zero byte
- overflow done with ASCIIZ string
	- prevents attacker from passing parameters to the function
	- prevents filling the buffer with a pattern