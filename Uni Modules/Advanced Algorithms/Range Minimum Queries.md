---
tags:
  - Lesson
  - range_minimum_queries
---
- preprocess an integer array $A$ of length $n$ to answer range minimum queries
	- a range minimum query is given by $RMQ(i,j)$ and outputs the location of the smallest element in $A[i,j]$
	- ideally we would like $O(n)$ space, $O(n)$ prep time and $O(1)$ query time
## Block Decomposition
### Solution 1
- $A_k$ is an array of length $\frac nk$ so that all $i:A_k[i]=(x,v)$ where $v$ is the minimum in $A[ik,(i+1)k]$ and $x$ is its location in $A$
	- store $A_k$ for all $k=1,2,4,8...\leq n$
	- this is $O(n)$ total space
	- $O(n)$ preprocessing time
		- you construct the $A_k$ arrays bottom-up, and you compute this from the two below in $O(1)$ time
	- if the amount of numbers is not a power of 2 you can just pad with $\infty$'s 
![[Screenshot 2024-10-27 at 15.05.44.png|300]]
- find $RMQ(i,j)$
	- find the largest block which is completely contained within the query interval but doesn't overlap a block you chose before and the minimum will be the smallest of these blocks
	![[Screenshot 2024-10-27 at 15.09.19.png|200]]
	- at most 2 blocks of each size will be selected
		- never two blocks of same size on one side
		- will never have gaps
		- there are $O(\log n)$ sizes and picking blocks from $A_k$ takes $O(1)$ time so we have:
			- $O(n)$ space
			- $O(n)$ prep time
			- $O(\log n)$ query time
### Solution 2
- precompute the answers for every interval of length $2,4,8,16,...$
	- array $R_2$ stores $RMQ(i,i+1)$ for all $i$, $R_4$ stores $RMQ(i,i+3)$ for all $i$ and $R_8$ stores $RMQ(i,i+7)$ for all $i$ ($R_k$ stores $RMQ(i,i+k-1)$ for all $i$)
- build $R_k$ for $k=2,4,8,16,...\leq n$ each of the $O(\log n)$ arrays uses $O(n)$ space so $O(n\log n)$ total space
	- we build $R_{2k}$ from $R_k$ in $O(n)$ time
	- this takes $O(n\log n)$ prep time
- to compute $RMQ(i,j)$:
	- if the interval length, $\mathscr{l}=(j-i+1)$, is a power-of-two we just look up the answer, there queries take $O(1)$ time
	- otherwise, find the $k=2,4,8,16,...$ such that $k\leq \mathscr{l}<2k$, compute the minimum of $RMQ(i,i+k-1)$ and $RMQ(j-k+1,j)$, this also takes $O(1)$ time
- we have:
	- $O(n\log n)$ space
	- $O(n\log n)$ prep time
	- $O(1)$ query time
## Low-resolution RMQ
**Key idea**: replace $A$ with a smaller, low resolution array $H$ and many small arrays $L_0, L_1,L_2,...$ for details
- $H$ has size $\tilde{n}$ space where $\tilde{n}=\frac n{\log n}$
- the smallest in each $\log n$ section in $A$ is stores in the corresponding slot in $H$
![[Screenshot 2024-10-27 at 15.47.04.png|400]]
- preprocess the array $H$:
	- $O(\tilde{n}\log\tilde{n})$ space $=O(n)$
	- $O(\tilde{n}\log\tilde{n})$ prep time $=O(n)$
	- $O(1)$ query time
- preprocess each array $L_i$:
	- $O((\log n)\log\log n))$ space/prep time
	- $O(1)$ query time
- total space = $O(n)+O(\tilde{n}\log n\log\log n)$ (space for RMQ structure for $H$ and space for RMQ structures for all the $L_i$ arrays) $=O(n\log\log n)$
- total prep time $= O(n\log\log n)$
- **answer a query in $A$**:
	- do at most one query in $H$ and one query in at most two different $L_i$ then take the smallest
	![[Screenshot 2024-10-27 at 15.55.27.png|300]]
		- $i'=[\frac i{\log n}]$ and $j'=[\frac j{\log n}]$ (indices into $H$)
		- here we query $L_1$ and $L_5$, this takes$O(1)$ total query time
- solution 3:
	- $O(n\log\log n)$ space
	- $O(n\log\log n)$ prep time
	- $O(1)$ query time
## Solving RMQs using LCAs
[[Lowest Common Ancestor]]
build the cartesian tree, $T_A$ of the array $A$:
- the root is the smallest value
- the selected location partitions the array in two
- the rest of the tree is given by recursing left and right
![[Screenshot 2024-10-31 at 14.05.23.png|300]]
>[!note]
this isn't very efficient, a better solution takes $O(n)$ time

**Key Fact**: the LCA in $T_A$ equals the RMQ in $A$
![[Screenshot 2024-10-31 at 14.06.36.png|200]]
- this gives us $O(n)$ space, $O(n)$ prep time and $O(1)$ query time for the RMQ problem