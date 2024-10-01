---
tags:
  - verification_tools
---
- treat sequential code constructs like general programming language
- all optimisations for language compilers apply:
	- data/control-flow analysis
	- global optimisations
		- limited because of model-build turn-around time requirements
	- local optimisations (loop unrolling, constant propagation)
	- register allocation
	- pipeline optimisations