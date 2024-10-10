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
	- ![[Screenshot 2024-10-10 at 12.41.23.png|300]]
	- Principle of operation:
		- compiler transforms combinatorial logic into boolean operations
		- compiler schedules inter-processor communications using a fast broadcast technique
		- performance is dictated by: