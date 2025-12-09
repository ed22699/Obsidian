---
tags:
  - Lesson
---
- cost of fixing hardware is big, cost of fixing software is cheap
	- when electrical engineers and computer architects mess up the software engineers end up having to fix it
## DRAM
- memory stores all the things the computer is thinking about that can't fit in a register
	- implemented using a capacitor and a transistor per bit
	- ganged (arranged) into long rows
	- placed into banks of ganged rows
- when we read to a bit of memory
	- find the row
	- activate the row by letting the capacitors discharge
	- this copies the row into an active memory buffer
- DRAM needs to be refreshed so the capacitors don't lose their charge over time
	- roughly every 64ms for modern hardware
- *issue*
	- capacitors leak charge
	- current in wires induces current in other nearby wires
	- the 1s and 0s aren't charged or uncharged capacitors
	- this was okay because electronic components were large 
	- as memory capacity increased the physical dimensions of memory have gotten smaller
### Rowhammer
- rowhammering is a bug in DRAM chips since 2010
	- if you repeatedly charge and discharge a row in DRAM really quickly it can cause errors in nearby rows
	- is treated more as a reliability issue then security issue
![[Pasted image 20251209163628.png|500]]
- if you perform the rowhammer with the above RAM layout eventually you'll get errors in the adjacent rows, this is single-sided rowhammering
- if you select X and Y so there is exactly 1 row between them eventually you'll get errors in the adjacent rows, quickly you'll get errors in the in-between row. This is double-sided Row Hammering
![[Pasted image 20251209163914.png|100]]
- it is not just all RAM which is susceptible to this, but that its all rows in all RAM (between 30-100%)
	- discover bit flips are consistent, even between the same RAM products
		- if Alice and Bob have the same make RAM from the same manufacturer then if they Rowhammer the same rows the same bits will always flip
- NaCl sandbox: Privileged sandbox for running native code from a we browser safely
	- X86 is a dense instruction set, different instructions have different lengths, some have multiple length
	- *Attack*:
		1. load a sequence of safe code that happens to be unsafe if you were to run it with a 1-bit offset
		2. rowhammer the loading code so that NaCl checks the code with no-offset, but runs it with an offset
		3. Outcome:
			- probably the program will crash because the loading code isn't valid
			- or we Rowhammer the kernel's memory and crash the entire computer
			- or it works
	- solution:
		- `clfush` is banned in NaCl loaded code
		- `clflush` is banned from non-root code (sometimes)
		- buy better RAM with 
			- error correction code (ECC)
				- expensive and slower (worth it for a server, not for a laptop)
				- still a potential denial of service/vulnerability if you can corrupt multiple bits at once with Rowhammer
			- refreshes faster
				- if you can't rowhammer faster than the refresh speed the attack doesn't work
				- but this slows down the whole computer
			- refreshes neighbouring rows more often
				- more recent DRAM standards do this
				- but again slows things down
## CPU Pipelines
![[Pasted image 20251209165123.png|400]]
- CPUs instructions take different times to complete as are pipelined
	- as one instruction is executing the next can be decoded and the next fetched
### Branch Prediction
- conditionals can cause a problem
	- e.g. can't load fetch the next multiply until we know if $n>0$ so pipeline stalls
- speculate that the loop is likely to be taken
	- CPU assumes it will be and fetches anyway
	- if assumption is wrong the CPU pipeline will have to be flushed before writeback but that should only happen once per call
	- speedup from removing the pipeline stall is bigger than the single pipeline flush, so performance gains (especially with symmetric multi-threading)