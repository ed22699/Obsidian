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
1. sort the items into non-increasing order
2. put each item in the first (left-most) bin it fits in
- FFD runs in $O(n^2)$ time
- how good is the approximation?
	- consider bin $j=[\frac {2s}3]$ ($s$ is the number of bins FFD uses on this input)
		- case 1: bin $j$ contains an item of size $> \frac 12$
			- every bin $j'\leq j$ contains an item of size $> \frac 12$ because we packed big things first and each thing was packed in the lowest number bin
				- each of these items has to be in a different bin (even in $Opt$)
			- so $Opt$ uses at least $\frac {2s}3$ bins or $s\leq \frac {3Opt}2$
		- case 2: bin $j$ contains only items of size $\leq \frac 12$
			- when FFD packed the first item into bin $j$
				1. all bins $j, (j+1),...,(s-2),(s-1)$ were empty
				2. all unpacked items had size $\leq \frac 12$ (as we pack in non-increasing order)
			- bins $j,(j+1),...,(s-2),(s-1)$ each contains at least two items and bin $s$ contains at least one item
			- gives a total of $2(s-j)+1$ items, none of which fits into bins $1,2,3,...,(j-1)$
			- so $I>\min\{j-1,2(s-1)+1\}\geq [\frac{2s}3]-1$ (by plugging in $j=[\frac{2s}3]$)
			- so $[\frac{2s}3]-1<I$ and $I\leq Opt$ we have that $[\frac{2s}3]-1<Opt$
				- as both sides are integers $[\frac{2s}3]\leq Opt$
				- finally $\frac {2s}3\leq[\frac{2s}3]\leq Opt$ or $s\leq (\frac 32)Opt$
		- in both cases $s\leq \frac{3Opt}2$
		- so FFD is a $3/2$-approximation algorithm for bin packing