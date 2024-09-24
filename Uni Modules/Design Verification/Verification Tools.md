---
tags:
  - Lesson
  - verification_tools
---
![[Screenshot 2024-09-24 at 09.55.50.png|300]]
# Automation
Task of Verification Engineer:
- ensure product does not contain bugs - done efficiently and cost-effectively
Task of Verification Team Leader
- select/provide appropriate tools
- select a verification team
- decide when cost of finding next bug violates law of diminishing returns
Parallelism, abstraction and automation can reduce the duration of verification
- automation reduces the human factor, improving efficiency and reliability
- Verification tools are use to achieve automation
	- Dynamic Verification
		- Hardware verification languages (HVL)
		- test-bench automation
		- test generators
		- coverage collection and analysis
		- general purpose HDL simulators (event-driven, cycle-based or waveform viewers)
	- Static Analysis/Verification Methods (Formal Methods)
		- linting tools
		- equivalence checkers
		- model checkers
			- property specification languages (ABV)
		- theorem proves
	- Administration
		- version control and issue tracking
		- metrics
		- data management and data mining related to metrics
	- Third party models
## Linting Tools
- static checkers
- assist in finding common coding mistakes
	- both for software and hardware (`gcc -Wall`)
- only identify certain classes of problems
	- false positives are reported so a filter program can be used to reduce these (try not to filter true positives)
- can assist in enforcing coding guidelines (rules can be added to linter)
>[!note] 
Still a use for linters as simulation-based testing may not simulate a situation which exposes the fault
## Simulators
- verification can be divided into two separate tasks
	1. Driving the design - controllability
	2. Checking its behaviour - observability
- questions:
	- am I driving all possible input scenarios?
	- how will I know when a failure has occurred?
- drivers - we cannot find bugs without creating the failing conditions
- checkers - we cannot find bugs without detecting the incorrect behaviour
### Test-bench
Code used to create a predetermined input sequence to a design, and to then observe the response
- refers to a test case/scenario
- traditionally refers to code written in a Hardware Description Language (VHDL, Verilog) at the top level of the design hierarchy
- is a completely closed system
	- no inputs or outputs
![[Screenshot 2024-09-24 at 12.47.08.png|300]]
### Simulation-based Design Verification
- simulate the design (not the implementation) before fabrication
- relies on simplifications (functional correctness/accuracy can be a problem)
Challenge: What input patterns to supply to the Design Under Verification (DUV) and knowing what is expected at the output for a properly working design
- Simulation requires stimulus. It is **dynamic**
- requires to reproduce the environment in which the DUV will be used (Testbench)
- simulation outputs are checked externally against the design intent (i.e. against the specification)
- errors cannot be proven not to exist "Testing shows the presence, not the absence of bugs"
## General HDL Simulators
- most popular - mentor graphics ModelSim/Questa, Cadence NCSim, Synopsys VCS
- provide support for full language coverage (event driven)
- to simulate with ModelSim:
	- compile HDL source code into a library
	- compiled design can be simulated
![[Screenshot 2024-09-24 at 13.03.30.png|400]]
![[Event-based simulators]]
# Simulation Speed
- bottle-neck for functional verification is simulation throughput
- can improve throughput with:
	- [[parallelisation]]
	- [[compiler optimisation techniques]]
	- [[changing the level of abstraction]]
	- methodology-based subsets of HDL (cycle-based simulation)
	- special simulation machines





car breaks and medical equipment 
controllability and observability worse in emulation
low level verification can be more thorough due to time limitations will need to use quicker methods on the higher levels