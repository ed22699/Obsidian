---
tags:
  - Lesson
---
- putting in guided random inputs to help understand the potential vulnerabilities of the system so they may be exploited
## Memory Corruption Vulnerabilities
- higher level code $\rightarrow$ low-level representation
- seemingly separate variables $\rightarrow$ contiguous memory addresses
	- contiguous memory locations allow for boundary violations
- e.g. use of `gets`, lead to:
	- over/underflow
	- sensitive data corruption 
	- control data corruption (control hijacking)
## Fuzzing
- security testing technique
- run program on many *abnormal/malformed* inputs, look for *unintended* behaviour e.g. crash
	- an observable (measurable) side effect is essential (such as the crash)
	- should be scalable (done in a reasonable time with a reasonable amount of code)
 *assumption*: if the unintended behaviour is dependent on input, an attacker can craft such an input to exploit the bug
 
### Types of Fuzzing
- **input based**
	- mutational and generative (grammar based)
	- *mutation based*: mutate seed inputs to create new test inputs
		- simple strategy is to randomly choose an offset and change the byte
		- pro: easy to implement and low overhead
		- con: highly structured inputs will become invalid quickly $\rightarrow$ low coverage
	- *generation (grammar) based*:
		- learn/create the format/model of the input
		- generate new inputs based on the learned model
		- e.g. well-known file formats (jpeg, xml, etc)
		- has a parsing phase (exploration of system) then an input phase (manipulation towards the crash)
		- pro: highly effective for complex structured input parsing applications $\rightarrow$ high coverage
		- con: expensive as models are not easy to learn or obtain
- **application based**
	- black-box and white-box
		- black-box: only interface is known
			- blackbox + mutation is aiming with luck (traditional fuzzing)
			- get better by apply more heuristics to 
				- mutate better
				- learn good inputs
			- apply more analysis (static/dynamic) to understand the application behaviour 
				- issue with this is the scalability factor
			- *solution*
				- smart or evolutionary fuzzing (educated guess)
				- rather than throwing inputs, *evolve them*
				- *assumption*: inputs are parsed enough before going further deep in execution
				![[Screenshot 2025-10-13 at 14.33.17.png|500]]
				- is a balancing act between blind-mutation/analysis/monitoring and scalability/performance	
					- scalability and performance cannot be negotiated much
				- what should be the feedback to evolve?
					- *code-coverage based fuzzing*
						- most of the contemporary fuzzers
							- AFL, AFLFast, Driller, VUzzer, ProbeFuzzer, CollAFL, Angora, QSYM, Nautilus
						- uses code-coverage as the proxy metric for the effectiveness of a fuzzer
					- *directed fuzzing*
						- not much explored
							- BuzzFuzz, AFLGo, ParmeSan
						- there should be a way to find the destination and sense of direction
		- whitebox: application can be analysed/monitored (e.g. open source)
- **input strategy**
	- memory-less and evolutionary