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
Still a use for linters as simulation-based testing may not provide a test which exposes the fault

car breaks and medical equipment 
controllability and observability worse in emulation
low level verification can be more thorough due to time limitations will need to use quicker methods on the higher levels