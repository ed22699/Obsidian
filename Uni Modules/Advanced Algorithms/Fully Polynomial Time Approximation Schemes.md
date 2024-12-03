---
tags:
  - Lesson
  - constant_factor_approx
---
# The Subset Sum Problem
![[Screenshot 2024-12-03 at 10.40.18.png|300]]
- let $S$ be a multi-set of positive integers and $t$ be a positive integer
- **Decision Problem**: Is there a subset $S' \subseteq S$ with size $t$
	- the size of $S'$ is $\sum_{a\in S'}a$
	- is NP-complete
- **Optimisation Problem**: find the size of the largest subset of $S$ which is no larger than $t$
	- is NP-hard
## Exact Solution
- let $S=\{s_1, s_2, s_3,...,s_m\}$ be the set of items and $S_i = \{s_1, s_2,...,s_i\}$
	![[Screenshot 2024-12-03 at 10.45.03.png|200]]
- Let $L_i$ be the set of sizes of all $s' \subseteq S_i$ which are not larger than $t$ (above $t=12$)
	- $L_3 = \{0,2,4,6,8,10\}$
	- the largest subset of $S$ (of size at most $t$) is the largest number in $L_m$
	- we compute $L_i$ from $L_{i-1}$: $L_i=L_{i-1} \cup (L_{i-1}+s_i)$ where $(x+s_i)\in (L_{i-1}+s_i)$ iff $x\in L_{i-1}$ and $x+s_i \leq t$
### Algorithm
- let $L_0=\{0\}$
- for $i=1...m$:
	- compute $(L_{i-1}+s_i)$ from $L_{i-1}$ ($O(|L_{i-1}|)$ time)
	- compute $L_i = L_{i-1}\cup (L_{i-1}+s_i)$ ($O(|L_{i}|)$ time)
- output the largest number in $L_m$ ($O(|L_{m}|)$ time)

- each $L_i$ is of length $|L_i| \leq t$, overall time complexity is therefore $O(mt)$
	- $n$ is the length of the input (measured in words)
		![[Screenshot 2024-12-03 at 10.56.37.png|400]]
	- the input to the subset sum problem is a list of the elements of $S$ along with $t$ encoded in binary in a total of $n$ words
	- as $m\leq n$, the time is $O(nt)$ but $t$ could be (for example) $2^n$, in other words $O(n2^n)$ time
# Pseudo-polynomial time algorithms
- we say that an algorithm is pseudo-polynomial time if it run sin polynomial time when all the numbers are integers $\leq n^c$ for some constant $c$
	- the algorithm for subset sum given takes $O(nt) =O(n^{c+1})$ time (in this case)
	- so there is a pseudo-polynomial time algorithm for subset sum
- we say that an NP-complete problem is weakly NP-complete if there is a pseudo-polynomial time algorithm for it 
	- the decision version of subset sum is weakly NP-complete
- we say that an NP-complete problem is strongly NP-complete if it remains NP-complete when all the numbers are integers $\leq n^c$ 
	- the decision version of Bin packing is strongly NP-complete
## Polynomial time approximation schemes (PTAS)
- PTAS for problem $P$ is a family of algorithms
	-  for any constant $\epsilon >0$ there is an algorithm in the family, $A_\epsilon$ such that $A_\epsilon$ is a $(1+\epsilon)$-approximation algorithm for $P$
- if we had a PTAS for subset sum we could 
	- let $\epsilon = 0.01$ so that $A_{0.01}$ also runs in polynomial time and outputs a subset of size at least $\frac {Opt}{1.01}>0.99\cdot Opt$
	- let $\epsilon = 0.001$ so that $A_{0.001}$ also runs in polynomial time and outputs a subset of size at least $\frac {Opt}{1.001}>0.999\cdot Opt$
- a PTAS does not have to have a time complexity which is polynomial in $1/\epsilon$
	- $A_{\epsilon}$ can have a time complexity of $O(n^{\frac{c}{\epsilon}})$ for example (above is $O(n^{1000c})$ for $\epsilon = 0.001$)
- a fully PTAS (FPTAS) has a time complexity which is polynomial in $1/\epsilon$ (as well as polynomial in $n$)
	- i.e. the time complexity is $O((n/\epsilon)^c)$ for some constant $c$ (above is $O((1000n)^c)=O(n^c)$ where $\epsilon = 0.001$)
## PTAS for subset sum
- recall that $L_i$ is the set of sizes of all $S' \subseteq S_i$ which are not larger than $t$ (where $S_i =\{s_1, s_2,...,s_i\}$ - the first $i$ numbers in the input)
- **Key Idea**: construct a trimmed version of $L_i$ (denoted $L_i' \subseteq L_i$) so that 
	- $L_i'$ is a subset of $L_i$
	- the length of $L_i'$ is polynomial in the input length (i.e. $|L_i'|\leq n^c$ for some $c$)
	- for every $y\in L_i$, there is a $z\in L_i'$ which is almost as big
- consider the process called trim
	- $Trim(L_i,\delta)$: include $L_i[j]$ in $L_i'$ iff $L_i[j] > (1+\delta)\cdot prev$ where $prev$ is the previous entry we included in $L_i'$
	- this doesn't achieve anything as we don't have time to compute $L_i$ and then trim it, instead we need to trim as we go along
- let $L_i$ be the set of sizes of all $S'\subseteq S_i$ which are not larger than $t$ - $L_i;$ is the trimmed version of $L_i$
	- let $L_0' = \{0\}, \delta = \epsilon/(2m)$
	- for $i=1...m$:
		- compute $(L_{i-1}'+s_i)$ from $L_{i-1}'$ ($O(|L_{i-1}'|)$ time)
		- compute $U=L_{i-1}' \cup (L_{i-1}' +s_i)$ ($O(|L_{i-1}'|)$ time)
		- let $L_i' = Trim(U,\delta)$ ($O(|L_{i}'|)$ time)
	- output the largest number in $L_m'$ ($O(L_{m}'|)$ time)
		![[Screenshot 2024-12-03 at 11.37.13.png|300]]
		- keep each thing if it is more than $(1+\delta)$ times as big as the last thing you kept
	- algorithm throws away some possible subsets, but it always outputs a valid subset (but probably not the largest one)
## $L_i$ vs $L_i'$
- **Lemma**: For any $y\in L_i$ there is an $z\in L_i'$ with $\frac y {(1+\delta)^i}\leq z \leq y$
- **Proof**:
	- base case: $L_0 = L_0' = \{0\}$
	- inductive step: assume that the lemma holds for $(i-1)$
		- as $y\in L_i$ we have that either $y\in L_{i-1}$ or $(y-s_i)\in L_{i-1}$
			- if $y\in L_{i-1}$ then there is a $x\in L_{i-1}'$ with $\frac y {(1+\delta)^{(i-1)}}\leq x \leq y$ 
	- by the definition of trim there is some $z\in L_i'$ with $z\leq z\leq z\cdot (1+\delta)