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
	- *writable*: you're allowed to change the value of memory
	- *executable*: you're allowed to run code from this memory
 - slower program loading as 2 extra systemcalls but is more secure
	 - mark code region as writable with `mprotect`
	 - load code into memory
	 - mark code as executable with `mprotect`
- one class of programs hate this (*JITing compilers*)
	- JavaScript and Java both compile programs on the fly a few instructions at a time
		- makes for really fast VMs
		- but two extra syscalls per JIT'd block means significant overhead
		- there is a mechanism to turn it off
## Why do we need to load code
- return to libc
	- the `system()` function does everything an `execve` shellcode does
		- and its already loaded into memory and marked executable
		- in 32bit cdecl calling conventions arguments to functions go via the stack
			- we can control with an overflow
![[Screenshot 2025-10-14 at 11.30.58.png|400]]
## Dealing with this
- return to libc works because
	- library functions are in predictable locations
	- arguments go via the stack which is corruptible
- fix
	- ASLR: we need to randomise stuff, but 32bit computers just don't have enough bits
	- Arguments: window's fastcall convention passes things via registers first and then the stack. So do syscalls, should maybe retire this
- either fix requires fundamentally changing how the OS and CPU work 
	- usually try to avoid this
	- create the new 64bit architecture
		- no more passing on the stack (by default)
		- loads of bits for randomisation
- randomness is still expensive
## Quick ASLR
- instead of loading each function into a random location load each library at a random offset
	- one random number per library instead of 1679
	- you can must `mmap()` in the whole library which is fast
	- you still don't know where the functions are precisely
- does mean that if a single pointer is leaked from that library, all pointers are leaked
	- you might not know where `fprintf` and `sscanf` are in memory but you know there are precisely `b0` bytes between them
![[Screenshot 2025-10-14 at 11.39.44.png|300]]
## Return to libc 2.0
- to use return to libc our attack chain is more complex
	1. find a buffer overflow
	2. break ASLR by leaking a pointer to a library
	3. return to `main` to restart the program without re-randomising 
	4. re-exploit buffer overflow to jump to the library function you now know the address of
![[Screenshot 2025-10-14 at 11.42.09.png|500]]
- why do we need to start a function at the beginning?
	- functions do a bunch of interesting stuff then `ret`
## Return Oriented Programming
![[Screenshot 2025-10-14 at 12.03.53.png|200]]
- a gadget is the stuff immediately before the `ret`
	- typically 1 or 2 instructions
	- if we could construct a brainfuck compiler out of just these gadgets then we could encode any program as a sequence of returns through the gadgets by dumping multiple return addresses on the stack with our overflow
		- if we cant to call `exit(0)` to crash a program early and cleanly
			- exit is syscall number 6
			- calling convention is syscall in `rax`, return code in `rbx`
			- we can use these gadgets to make the syscall by returning back through 10 instructions
![[Screenshot 2025-10-14 at 12.05.19.png|400]]
- start with an overflow onto a return address
- stick our ROP chain on the stack and start returning
![[Screenshot 2025-10-14 at 12.06.40.png|500]]
- this writes an entire program by writing shellcode as a path through pre-existing code in our program
	- arbitrary code execution purely through reuse
	- most sufficiently large programs will contain enough usable gadgets that arbitrary code can be loaded
## How do we stop this
- ROP falls out from fundamental decisions about how computers were architected that we made back in the 60s
	- Von Neumann vs Harvard architectures
- we can't stop this trivially
- few techniques that make it harder
	- *shadow stacks*: keep a second stack for stack consistency checking and have the kernel kill the program if it ever gets out of sync
	- *full ASLR*: really randomise everything
	- *Instruction Pointer Integrity Protections*: on return check that our instruction pointer goes only to whitelisted addresses (or is aligned)
	- just fix the buffer overflow
		- Rust/Zig
		- not using unsafe languages 
- OpenBSD project deployed a technique called *Branch Target Identification* to their entire OS
	- compiler works out everywhere that you could jump to as the result of an indirect jump
		- a jump that depends on a variable (i.e. a function pointer loaded from a register)
	- add a `endbr64` instruction (on x64) to the target
	- if you don't encounter an `endbr64` instruction kill the program
	- gadgets now have to start with an `endbr64` instruction
		- typically are just entry points to a whole function
		- much harder to find a useful set of gadgets
			- so can't divvy up functions as before
		- technically it breaks a more practical variant of ROP called JOP which uses jump tables to do something similar
		- this plus stack canaries makes ROP tricky though
		- this plus syscalls only through `libc` wrappers makes it really hard