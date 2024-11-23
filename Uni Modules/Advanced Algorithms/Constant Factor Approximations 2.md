---
tags:
  - Lesson
  - constant_factor_approx
---
[[Constant Factor Approximations]]
## Scheduling Jobs On Parallel Machines
**Aim**: minimise the wall-clock time taken to process all jobs
![[Screenshot 2024-11-23 at 13.34.21.png|400]]
- NP-hard
![[Screenshot 2024-11-23 at 13.35.40.png|400]]
- job $j$ takes $t_j$ time units
- $j\in J(i)$ iff job $j$ is assigned to machine $i$
- the load of machine $i$ is $L_i=\sum_{j\in J(i)}t_j$
- wall-clock time is $\max_iL_i$
- **Algorithm 1**: 
	- put job $j$ on the machine $i$ with smallest (current) load
	- $m$ machines, $n$ jobs $\Rightarrow O(nm)$ time naively, $O(n\log m)$ time using priority queue
	- online solution
	- how good? (2-approximation algorithm)
		- let $Opt$ denote the time taken by the optimal scheduling of jobs
		- let $T_g$ denote the time taken by the greedy schedule
		- $Opt\geq \max_j t_j$ (some machine must process the largest job)
		- $Opt \geq \frac{\sum_j t_j}m$
			- total of $\sum_j t_j$ time units of work to be done
			- some machine $i$ must load $L_i$ at least $\frac{\sum_j t_j}m$ (the $m$ machines can\t all have below average load)
		- **Proof**: consider the machine $i$ with largest load $T_g=L_i$
			- let $j$ denote the last job machine $i$ completes
			- when job $j$ was assigned, machine $i$ had the smallest load $L_i-t_j$