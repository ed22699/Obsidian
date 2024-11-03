---
tags:
  - Lesson
  - constant_factor_approx
---
polynomial time - $O(n^c)$
[[NP-completeness]]
# Bin Packing
**Problem**: pack all items into the fewest possible bins (optimisation problem)
![[Screenshot 2024-11-03 at 11.07.48.png|400]]
- Bin Packing problem is known to be $NP$-hard
	- decision version "can you pack the items into at most $k$ bins" is $NP$-complete ($k$ is part of the input)
- **Solution**: approximate
## Approximation Algorithms
- algorithm $A$ is an $\alpha$-approximation algorithm for problem $P$ if:
	- $A$ runs in polynomial time
	- $A$ always outputs a solution with value $s$ within an $\alpha$ factor of $Opt$
- here $P$ is an optimisation problem with optimal solution of value $Opt$
	- if $P$ is a maximisation problem $\frac {Opt}\alpha\leq s\leq Opt$
	- if $P$ is a minimisation problem (like bin packing) $Opt\leq s\leq \alpha\cdot Opt$
- in examples we consider $\alpha$ a constant but it could depend on $n$ 
## Next fit
- if item $i$ fits into bin $j$: pack it, `i++`; else `j++`;
	- runs in $O(n)$ time where $n$ is the number of items
- how good is the approximation?
	- let $fill(i)$ be the sum of item sizes in bin $i$ and $s$ be the number of non-empty bins 
	- observe that $fill(2i-1)+fill(2i)>1$ for $1\leq 2i\leq s$ ($2i - 1$ and $2i$ are two bins next to each other)
	- so $[\frac s2]<\sum_{1\leq 2i\leq s}fill(2i-1)+fill(2i) \qquad \leq I\leq Opt$
		- $I$ is the sum of the item weights 
		- $Opt$ is the optimal number of bins
		- therefore $s\leq 2\cdot Opt$ (next fit is never worse than twice the optimal)
			- this is a $2$-approximation algorithm
## First Fit Decreasing (FFD)