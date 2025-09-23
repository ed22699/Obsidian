---
tags:
  - interesting_bugs
---
```c
int main(int argc, char *argv[]) { 
	printf("This program is called: "); 
	printf(argv[0]); // What! You never heard of %s? 
	printf("\n"); 
	return 0; 
}
```
- if we name our program something silly like `%08x-%08x-%08x-%08x`
	- returns `This program is called: ./000120a8-00000000-118a0041-4f6d0188`
- printf assumes you know what you're doing
- gives us a mechanism for dumping whats on the stack (and potentially registers) and leaking information
	- can be used to return an address
![[Screenshot 2025-09-23 at 12.11.49.png|500]]
