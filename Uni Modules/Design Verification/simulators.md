---
tags:
  - verification_tools
---
- verification can be divided into two separate tasks
	1. Driving the design - controllability
	2. Checking its behaviour - observability
- questions:
	- am I driving all possible input scenarios?
	- how will I know when a failure has occurred?
- drivers - we cannot find bugs without creating the failing conditions
- checkers - we cannot find bugs without detecting the incorrect behaviour
### Test-bench
![[testbench]]
### Simulation-based Design Verification
- simulate the design (not the implementation) before fabrication
- relies on simplifications (functional correctness/accuracy can be a problem)
Challenge: What input patterns to supply to the Design Under Verification (DUV) and knowing what is expected at the output for a properly working design
- Simulation requires stimulus. It is **dynamic**
- requires to reproduce the environment in which the DUV will be used ([[testbench]])
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
## Cycle-based simulators
![[Cycle-based simulators]]

## Hardware Acceleration
![[Hardware Acceleration]]

## Simulation Speed Comparison
| Simulator                    | speed (relative to event-based) |
| ---------------------------- | ------------------------------- |
| [[Event-based simulators]]   | 1                               |
| [[Cycle-based simulators]]   | 20                              |
| Event-driven cycle Simulator | 50                              |
| [[Hardware Acceleration]]    | 1000                            |
| Emulation                    | 100000                          |
- controllability and observability worse in emulation
- low level verification can be more thorough, however, due to time limitations will need to use quicker methods on the higher levels