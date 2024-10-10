---
tags:
  - verification_tools
---
### Hardware acceleration
- programs created for cycle-based simulation are very simple
	- small set of instructions
	- simple control (no branches, loops or functions)
- operations at the same level can be executed in parallel [[levelization]]
	- [[scheduling]]
exploit theses facts for fast simulation by utilising
- very large number of small and simple special-purpose processors
	- Logic Processing units (LPs) are special purpose processing units that are much faster than the CPUs
	- each cluster has its LPs connected in array to allow fast communication
	- in addition these clusters are laid out in a fast communication infrastructure so all these different units are together making it really fast
	- ![[Screenshot 2024-10-10 at 12.41.23.png|300]]
	- to map this design onto an accelerator we need a compiler
	- Principle of operation:
		- compiler transforms combinatorial logic into boolean operations
		- compiler schedules inter-processor communications using a fast broadcast technique
		- performance is dictated by:
			- number of processors (LP units)
			- number of levels in the design