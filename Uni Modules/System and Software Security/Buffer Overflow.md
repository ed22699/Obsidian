---
tags:
  - interesting_bugs
---
- in C if you go over the end of an array you'll crash (buffer overflow)
### Segmentation faults
- Memory in a binary get split into sections
	- if you attempt to write in memory without having the permission the MMU will trigger an exception to the OS and the program will crash with a segfault
![[Screenshot 2025-09-22 at 15.41.30.png|500]]
- sometimes you don't go too far off the end of an array and the fault does not trigger
```c
void function(char *str) {
	char buffer[16]; 
	strcpy(buffer, str); 
} 
void main() { 
	char large_string[256]; 
	int i; 
	for (i=0; i<255; i++) 
		large_string[i] = 'A'; 
	function(large_string); }
```
- will fill the buffer with A
- then will overwrite whatever else is on the stack
- then will overwrite whatever else until the segfault happens
- Aim to *stop before the segfault*
![[Screenshot 2025-09-22 at 15.45.44.png|500]]
- here the return address will be loaded into emory and we'll start executing from 0x41414141 (A in ASCII is byte 0x41)
- if you are smart you can aim to return something more useful
	- stack addresses are usually predictable
	- you can put in the butter something that corresponds to program code
	- trick computer into running *arbitrary code execution*
### Assumptions
- you have assumed the program will crash just because that's what its supposed to do
- how do we stop it?
	- make addresses less predictable (*ASLR*)
	- stick a canary in the stack and check it hasn't been overwritten before returning (*stack canaries*)
	- use a research grade CPU architecture like CHERI that doesn't allow you to abuse pointers like this
	- use [[branch targets]]