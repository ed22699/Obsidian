---
tags:
  - Lesson
---
- we like to create objects dynamically in memory
	- need to talk to the OS and ask it to give more or less memory
	- POSIX has a set of standard system calls
		- `mmap` maps devices and files into a program's running memory
		- `mprotect` lets us set usage policies about memory
		- `brk & sbrk` (mostly depreciated) for controlling how big the program data is
	- issue is this is really slow
- *Malloc*: instead of going to the kernel every time we want to manage memory we'll give a program a reasonable chunk of memory in its virtual address space and an API for managing it
	- can call the system calls if necessary 
	- we base it on a heap data structure and call it the heap
	- call it `malloc` and `free`
	- *issue*: every OS has a slightly different implementation
![[Screenshot 2025-10-05 at 18.36.31.png|200]]
- Its vulnerability:
	- can overwrite the function pointer with `strcpy`, can change this to the address of the function we actually want to call
	- is just a buffer overflow just in a different location
	- more generally
		- buffers exist on the heap
		- we can over and under flow them
		- sometimes you hit something useful
- when memory gets allocated and deallocated extra stuff gets written to the heap
	- data gets written into the heap based on this data on a `free()`
	- `malloc()` is probably using it to work out where the free sections are
	- `free()` can be abused to write to an arbitrary pointer
### How
- memory starts out as a big arena region of memory for the program's heap; shared among threads
- each heap belongs to one arena and is divided into *chunks* which are small ranges of memory that can be allocated from
![[Screenshot 2025-10-05 at 18.42.44.png|500]]
- as memory gets used by programs it gets more and more chunked up
- to deal with this `free()` will merge chunks when releasing the memory
	- if the `bck` chunk is free it'll go back and update the size to include both of them
	- it'll update the `bck` chunk's `fwd` pointer to be this chunks `fwd` pointer merging the two chunks
	- it'll update the `fwd` chunk's `bck` pointer to be the new merged chunk
![[Screenshot 2025-10-05 at 18.45.51.png|500]]
- once a chunk has been used, it is released back into the free pool
	- means a process can reuse that memory for future allocations
![[Screenshot 2025-10-05 at 18.48.14.png|500]]
![[Screenshot 2025-10-05 at 18.48.44.png|500]]