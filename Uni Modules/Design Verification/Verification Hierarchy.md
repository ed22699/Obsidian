---
tags:
  - Lesson
  - VerificationHierachy
---
- black box
- white box
- grey box
# Observability and Controllability
- Observability: Indicates the ease at which the verification engineer can identify when the design acts appropriately versus when it demonstrates incorrect behaviour 
	- how easy it is to tell the difference between well designed and poor design
	- [[black box]]: nothing visible
	- [[white box]]: everything visible
	- [[grey box]]: some visible
- Controllability: Indicates the ease at which the verification engineer creates the specific scenarios that are of interest
	- how easy to set up so I can focus on the design
	- grey and white boxes can have unreachable states
		- problem of unreachable states - testing things that will never be reachable in practice (finding bugs that don't exist), can lead to people in the design team not taking you seriously 
		- can lead to an inconsistent DUV state
		- Exception - Warm loading:
			- brings the DUV to a predefined interesting state (e.g. cache initialisation, almost full buffer)
			- reduces the time needed for reaching the state
# Verification Hierarchy
- complex chips are systems are divided into logical units
	-  determined during specification / high-level design
	- follow the architecture of the system
	- practice is called hierarchical design
		- allows designer to subdivide a complex problem into more manageable blocks (combine blocks to form bigger units up to chip or system is complete)
		- pros: breaks design into manageable pieces, allow designers to focus on single function / aspect of the design
		- cons: more interfaces to specify/design/verify and more integration issues
- verification takes advantage of hierarchical design stages and boundaries by splitting into levels of verification:
	- [[Designer level (block level)]]
	- [[Unit level]]
	- ([[Core level]])
	- [[Chip level]]
	- [[System level]]
	- [[Hardware and software co-verification]] (beyond course scope)
- system - coverage usually only a good method at lower levels, higher levels should focus on test cases (core level up)
- always choose the lowest level that completely contains the target function under verification
- each verifiable piece should have its own specification 
- function to be verified may dictate the appropriate level for verification
- selected level must provide suitable controllability and observability to perform verification
![[Screenshot 2024-09-17 at 21.33.47.png|600]]
- Only move up to the next level when the number of bugs found at the current, lower, level has started to drop
## Which levels to verify?
- each level that is exposed to the "outside world" is mandatory (e.g. chip level, system level)
- rest depends on complexity, risk, schedule and resources
