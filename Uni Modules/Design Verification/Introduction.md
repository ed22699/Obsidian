---
tags:
  - Lesson
  - intro
---
Design Verification is the process used to gain confidence in the correctness of a design w.r.t. the requirements and specification
![[verification methods.png|300]]
- Many different methods can be used to gain the is confidence 
- Ensure requirements and specification are given if you want to verify a system
## Verification (looks at behaviour) 
- confirms that a system has a given input / output behaviour, sometimes called the transfer function of a system
- role of verification to confirm that the system implements exactly that transfer function
- in order to perform verification you need to know what the transfer function is (how inputs are transferred to output) and that what the system does given the inputs conforms to what the specification says it should do in order to produce the output 
## Validation (looks at purpose)
- Confirms that the system's transfer function results in the intended system behaviour when the system is employed in its target environment, e.g. as a component of an embedded system
- Is the system fit for purpose? What is the intended behaviour when used in its target environment?
# The IC Design Process
![[icDesignProcess.png|400]]
- **Architectural Specification**: Specifies the processors states and instruction set (usually a reference manual)
- **Micro Architectural Design**: How the instruction set is implemented
- **RTL Model**: (Register Transfer Level) written in a hardware description language like Verilog or VHDL
- **Gate-Level Model**: 
- **Transistor-Level Model**: 
- **Layout**: How fast and long the signals have to travel in the physical implementation (about real time units)
- **Mask Data**: Entry point for the chip manufacturing process
- **Behavioural Model**: A cycle accurate model, executes a sequence of instruction in a specified number of clock cycles (about clock cycles)
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
 ![[verification and test.png|300]]
## Design For Test
- one method is scanning:
	- link all internal registers together into a chain
	- chain accessible from chip pins
	- allows control/observation of internal state
	- impacts area of design, but keeps testing costs down
- means manufacturers can prove that it is not their chip which is at fault, can show that all transistors are working outside the designs function and can show the speed of different chips 
- if fabrication is correct either design is incorrect or timing is wrong
 ![[Screenshot 2024-09-17 at 11.43.16.png|300]]
## Equivalence Checking
Compares two models to heck for equivalence
- proves mathematically that both are logically equivalent (commonly used on lower levels of design process) e.g. RTL to Gates
- conceptually asking "is there an input vector such that the output of the XOR gate can be 1?"
![[Screenshot 2024-09-17 at 11.46.04.png|250]]
# Cost of Verification
- always takes too long and costs too much
- as number of bugs found decreases, cost and time of finding remaining ones increases
- verification does not generate revenue
- indispensable 
	- ensures functionally correct design and provides benefits to customer
	- proper functional verification demonstrates trustworthiness of the design
	- right-first-time designs demonstrate professionalism and increase reputation
![[Screenshot 2024-09-17 at 11.50.04.png|500]]
