---
tags:
  - interesting_bugs
---
- implemented as part of Intel's control-flow enforcement technology
- whenever you make an indirect jump you have to land on an endbr64 instruction, when you return from a function you have to check the stack hasn't been meddled with
	- kernel has to keep its own copy for each process to check against
	- solves everything