---
tags:
  - Article
---
- on many C implementations it is possible to corrupt the execution stack by writing past the end of an array declared auto in a routine
	- code doing this is said to *smash the stack*
		- can cause the return from a routine to jump to a random address
- is a *buffer overflow vulnerability*
	- examples syslog, splitvt, sendmail 8.7.5
- paper assumes Intel x86 CPU with OS being Linux
- static variables are allocated at lode time on the data segment
- dynamic variables are allocated at run time on the stack
- we concern ourselves with the overflow of dynamic buffers (stack-based buffer overflows)
### Process Memory Organisation
- processes are divided into three regions
	- Text - fixed by the program, includes code and read-only data
		- writing here is a segmentation violation
	- Data - contains initialised and uninitialised data. Static variables
		- new memory is added between the data and stack segments if this needs to grow
	- Stack
		- the stack is needed for higher level languages which make use of functions. Functions disrupt the flow of control, hence need to be put onto the stack and have control returned after when pushed off the stack
		- also used to dynamically allocated the local variables used in functions, to pass parameters to the functions, and to return values from the function
![[Screenshot 2025-09-24 at 22.36.11.png|200]]
## The Stack Region
- contiguous block of memory containing data
- A register called the *stack pointer* (SP) points to the top of the stack
- the bottom of the stack is at a *fixed address*
- size dynamically adjusted at run time by the kernel
- stack consists of *stack frames*
	- contains the parameters to a function, its local variables, and the data necessary to recover the previous stack frame, including the value of the instruction pointer at the time of the function call
- depending on the implementation the stack will either grow down (towards lower memory addresses), or up. SP is also implementation dependent, can point to next free address after the stack or the last address on the stack
	- most implementations grow down
	- assume SP points to last address on stack
- *frame pointer* (FP) points to a fixed location within a frame (also called a local base pointer (LB)), many compilers use this second register for referencing both local variables and parameters as their distances from FP do not change with Pushes and Pops
- first thing a procedure must do when called is save the previous FP
	- then copies SP into FP to create new FP
	- advances SP to reserve space for the local variables
	- procedure epilogue cleans this up upon procedure exit
	- LINK and UNLINK or ENTER and LEAVE are used
```c
void function(int a, int b, int c) {
   char buffer1[5];
   char buffer2[10];
}

void main() {
  function(1,2,3);
}
```
```x86
; Call to function
pushl $3 ; Pushes the 3 arguments
pushl $2 ; Pushes the 3 arguments
pushl $1 ; Pushes the 3 arguments
call function ; push the instruction pointer (IP onto the stack)

; The Function
pushl %ebp ; pushes EBP (frame pointer) onto the stack
movl %esp,%ebp ; copies the current SP onto EBP, making it the new FP pointer
subl $20,%esp ; allocates space for the local variables by subtracting their size from SP
```
