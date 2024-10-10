---
tags:
  - verification_tools
---
- environment used for verification before fabrication
Code used to create a predetermined input sequence to a design, and to then observe the response
- refers to a test case/scenario
- traditionally refers to code written in a Hardware Description Language (VHDL, Verilog) at the top level of the design hierarchy
- is a completely closed system
	- no inputs or outputs
	- is essentially a model of the universe
![[Screenshot 2024-09-24 at 12.47.08.png|300]]
- testbench makes up 80% of the design and so bugs may be in the testbench rather than the DUV