---
tags:
  - Lesson
  - code_coverage
---
why only provide stopping criteria for unit testing?
- unrealistic with the given time and effort
proving dead code
- collect conditions, negate them and pass into formal tool, either proves it is dead code or be given a counter example
	- expensive
exhaustive to modified reduces the number of cases required $2^n \rightarrow n+1$

mutation testing - if I change the code slightly will the test suit flag the change (create many mutants with minor errors and test against the test suit)
- make sure not semantically the same, syntactically different mutants
- way to gain confidence in someone else's testing campaign 
