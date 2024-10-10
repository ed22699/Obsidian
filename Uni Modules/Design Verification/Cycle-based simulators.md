---
tags:
  - verification_tools
---
## Synchronous design methodology
- design comprised of 
	- state-holding elements
	- combinational logic for state transition function
![[Screenshot 2024-09-24 at 13.38.53.png|400]]
# Cycle-based model build flow
1. language compile 
	- synthesis-like process
		- simpler as missing physical constraints
		- logic is mapped to a non-cyclic network of boolean functions
		- hierarchy is preserved during language compilation
2. flatten hierarchy 
	- crush design hierarchy to increase optimisation potential
3. optimisation 
	- minimise the size of the model to increase simulation performance
4. Levelize logic
	- [[levelization]]
5. translate to dedicated instructions
	- convert every boolean function into a minimal set (4 or better) of dedicated instructions
	![[Screenshot 2024-10-10 at 12.18.26.png|200]]
- word-level operations can be easily parallelised
## Speed
- clock cycle in design is only as fast as the longest possible combinational delay path settles before the cycle is over
	- cycle time depends on the longest topological path
		- calculated using static analysis without simulation as stronger result
	![[Screenshot 2024-10-10 at 12.32.13.png|300]]
can be sped up with [[Hardware Acceleration]]