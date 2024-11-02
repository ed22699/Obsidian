---
tags:
  - constant_factor_approx
---
$NP$ is the class of decision problems we can check the answer to in polynomial time ($O(n^c)$)
- problem $A$ is $NP$-complete if:
	- $A$ is in $NP$
	- every $B$ in $NP$ has a polynomial reduction to $A$ (definition of $NP$-hard)
		- we can solve $B$ using $A$
>[!note]
decision problems are yes/no problems

- if we could solve $A$ quickly we could solve every problem in $NP$ quickly
	- there are the 'hardest' problems in $NP$
- most believe that you can't solve $NP$-complete problems in polynomial time ($P\neq NP$)