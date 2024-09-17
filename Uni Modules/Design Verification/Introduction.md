---
tags:
  - Lesson
  - intro
---
Design Verification is the process used to gain confidence in the correctness of a design w.r.t. the requirements and specification
![[verification methods.png|300]]
- Many different methods can be used to gain the is confidence 
- Ensure requirements and specification are given if you want to verify a system
## Verification ----
- confirms that a system has a given input / output behaviour, sometimes called the transfer function of a system
## Validation ----
- Confirms that the system's transfer function results in the intended system behaviour when the system is employed in its target environment, e.g. as a component of an embedded system
# The IC Design Process
![[icDesignProcess.png|400]]
- **Architectural Specification**: -----------------
- **Micro Architectural Design**: 
- **Behavioural Model**: 
- **RTL Model**: 
- **Gate-Level Model**: 
- **Transistor-Level Model**: 
- **Layout**: 
- **Mask Data**: 
- **Design Library**: 
- Functional verification aims to demonstrate that the functional intent of a design is preserved in its implementation
# Why is Verification Important
Verification is the single biggest lever to effect the triple constraints:
- Quality
	- high quality track record preserves revenue and reputation
	- ideally a team can establish a "right-first-time" track record
- Cost
	- fewer revisions through the development/fabrication process means lower costs
	- respinning a chip costs hundreds of thousands
- Timing/Schedule
	- fewer revisions through the development/fabrication process means faster time-to-market
	- respinning a chip costs 6-8 weeks at least
# Bugs
- bugs that remain hidden can cause late to market cost, lost opportunity cost, loss of reputation, mask costs, debug costs and recall costs
- the longer a bug goes undetected, the ore expensive it is
# Complexity
![[complexity.png|500]]
- As more transistors were added to chips this increased the design complexity. Instead of utilising all transistors in a design the hardware designers instead opted to duplicate a design, creating cores. This shifts the issue of complexity onto the software designers, however, is a more forgiving and less costly area of errors
# Role of Verification in IC Design
- Engineers need to balance conflict of interest:
	- tight time-to-market constraints vs increasing design complexity
- aim for "right-first-time" design, "correct-by-construction"
- more and more time-consuming to obtain acceptable level of confidence in correctness of design
- design time < verification time
	- up to 70% of design effort can go into verification
	- 80% of all written code is often in the verification environment
	- verification does not create value, but preserves reputation
	- in some cases verification engineers outnumber designers 1:2
# Increasing Verification Productivity
minimise verification time by:
- parallelism: add more resources
- abstraction: higher level of abstraction (often reduction of control)
- automation: 
	- tools automate standard processes
	- requires standard processes/methodology
	- variety of functions, interfaces, protocols and transformations must be verified
	- not all verification processes can be automated
Productivity improvements drive early problem discovery
# Chip Design Process
![[chipDesignProcess.png|500]]
![[verifyAndTest.png|500]]
- testing usually occurs after the manufacturing of the chip has occurred
# Reconvergence Models
## What are you verifying?
- purpose of verification is to ensure that the result of some transformation is as intended or as expected 
- purpose of test is to show design was manufactured properly
- verification is done to ensure that design meets its functional intent prior to manufacture
 ![[Screenshot 2024-09-17 at 11.38.39.png]]