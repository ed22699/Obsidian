---
tags:
  - verification_tools
---
- static checkers
- assist in finding common coding mistakes
	- both for software and hardware (`gcc -Wall`)
- only identify certain classes of problems
	- false positives are reported so a filter program can be used to reduce these (try not to filter true positives)
- can assist in enforcing coding guidelines (rules can be added to linter)
>[!note] 
Still a use for linters as simulation-based testing may not simulate a situation which exposes the fault