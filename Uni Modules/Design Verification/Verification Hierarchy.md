---
tags:
  - Lesson
  - VerificationHierachy
---
- black box
- white box
- grey box
# Observability and Controllability
- Observability
	- how easy it is to tell the difference between well designed and poor design
	- black box: nothing visible
	- white box: everything visible
	- grey box: some visible
- Controllability
	- how easy to set up so I can focus on the design
	- problem of unreachable states - testing things that will never be reachable in practice (finding bugs that don't exist), can lead to people in the design team not taking you seriously 
# Verification Hierarchy
designer level verification - small enough for programmers to run basic verification themself
unit level - first level of serious verification

system - coverage usually only a good method at lower levels, higher levels should focus on test cases

begin top level tests after you have reached the peak of unit level tests bugs found
after you've reached the peak of the lower level bugs found you can move to the higher level