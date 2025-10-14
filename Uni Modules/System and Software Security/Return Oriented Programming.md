---
tags:
  - Lesson
---
```c
void greet() {
	char name[4];
	printf(”Who should I greet ? ”);
	gets(name);
	printf(”Hello %s ! \ n ” , name);
}
```
- first we call it by saving where we were and sticking it on the stack (SIP) and loading the address of greet() into rip
![[Screenshot 2025-10-14 at 11.09.57.png|300]]
- create a new stack frame
	- we need to save the previous stack frame so we need enough space for the current base pointer, plus space for the 4 chars of the name
![[Screenshot 2025-10-14 at 11.11.14.png|300]]
- make the three function calls to `printf()`, `gets()` and `printf()`
![[Screenshot 2025-10-14 at 11.13.10.png|300]]
- leave any leftover data in the stack wilderness by moving the stack pointer back up
![[Screenshot 2025-10-14 at 11.14.13.png|300]]
- we then restore the previous stack frame by popping the stack into the base pointer (move the ebp)
- we restore the instruction pointer by popping the stack into the instruction pointer (move the esp)
![[Screenshot 2025-10-14 at 11.15.56.png|300]]
## Smashing the stack
- because of the `gets()` the program is vulnerable to smashing the stack
	- if we overflow the buffer the return address can be overwritten and we can crash when we try to return 
- shellcoding
	- stack addresses are easy to guess
		- if we arrange for there to be program code where we're returning to we can trick the program into running it for us
![[Screenshot 2025-10-14 at 11.19.31.png|300]]
- *issues*:
	- ASLR (why is it so easy to guess where the stack is)
		- if we make it random, then it should be harder to guess exactly where things are
			- randomness is very expensive
			- randomising things costs time at program startup
			- 32-bit x86 has limited numbers of bits for doing randomness
	- $W \oplus X$ (why are we running code off the stack)
		- $W \oplus X$ writable or executable 
		- program code shouldn't exist on the stack
			- can implement the protection in hardware 
## $W \oplus X$
- for each page of program memory, add an extra bit. Memory can be marked as either writable or executable
	- 