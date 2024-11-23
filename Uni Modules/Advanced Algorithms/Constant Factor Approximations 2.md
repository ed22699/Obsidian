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
- **Algorithm (greedy approx)**: 
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
			- when job $j$ was assigned, machine $i$ had the smallest load $L_i-t_j$ so $L_i-t_j\leq L_k$ for all $1\leq k\leq m$
			- if we sum over all $k$ then $m(L_i-t_j)\leq\sum_{k=1}^mL_k$ so 
				- $(L_i-t_j)\leq\frac{\sum_{k=1}^mL_k}m\leq Opt$
				- $t_j\leq Opt$
				- therefore $T_g=L_i=(L_i-t_j)+t_j\leq Opt+Opt=2\cdot Opt$
- **Algorithm (Longest Processing Time)**:	
	1. sort jobs into non-increasing order (job 1 is now the largest)
	2. put job $j$ on the machine $i$ with smallest (current) load
	- $O(n\log n)$ time
	- how good? ($3/2$-approximation algorithm)
		- if there are at most $m$ jobs ($n\leq m$) then LPT is optimal, if there are at most $m$ jobs then LPT gives each job its own machine so $\max_iL_i\leq \max_jt_j\leq Opt$
		- if $n > m$ then $Opt\geq 2t_{(m+1)}$
			- $t_1\geq t_2\geq t_3\geq ... \geq t_{(m+1)}$
			- one of the $m$ machines must be assigned at least two of these $m+1$ jobs under any schedule
			- we have that any schedule takes at least $2t_{(m+1)}$ time in particular $Opt\geq 2t_{(m+1)}$
		- **Proof**: consider the machine $i$ with largest load $T_l=L_i$
			- let $j$ denote the last job machine $i$ completes
			- using the same argument as before we have that $(L_i-t_j)\leq Opt$
			- if $n\leq m$ then we are done so assume $n>m$
			- further if $(L_i-t_j)=0$ then $T_l=L_i=t_j\leq Opt$ so assume that $(L_i -t_j)>0$
			- therefore machine $i$ was assigned at least two jobs by the algorithm description, we have that $j\geq m+1$ and $t_j\leq t_{m+1}\leq Opt/2$ (by the lemma)
			- therefore $T_l=L_i=(L_i-t_j)+t_j\leq Opt+Opt/2=(3/2)\cdot Opt$
		- in fact, LPT is a $4/3$-approximation algorithm (using better analysis)
## K-centres
![[Screenshot 2024-11-23 at 14.09.45.png|400]]
![[Screenshot 2024-11-23 at 14.10.43.png|300]]
- we want to minimise $r$, which is the longest distance to a point in a cluster
- **Algorithm (greedy approximation)**:
	- start by picking any point to be a centre 
	- repeatedly pick the site which is furthest from any existing centre
	- **Proof**: 2-approximation algorithm
		- let $C_g$ denote the set of centres selected by greedy
		- let $r_g$ denote the largest site-centre distance using greedy
		- **case 1**: no $s_i, s_i' \in C_g$ are closest to the same $s_j\in C_{Opt}$
			![[Screenshot 2024-11-23 at 14.16.59.png|300]]
		- **case 2**: some $s_i, s_i'\in C_g$ are closest to the same $s_j\in C_{Opt}$
				![[Screenshot 2024-11-23 at 14.22.53.png|100]]
			- $s_i$ was added as a centre because it was the furthest from any existing greedy centre
			- however, $s_i$ is at most $2Opt$ away from $s_i'$
			- so even before adding $s_i$ as a centre, all sites were $\leq 2Opt$ away from a greedy centre therefore $r_g\leq 2Opt$
		- **Theorem**: the greedy algorithm for $k$-centre is a 2-approximation algorithm which runs in $O(nk)$ time
			- approximation works for any metric distance function $d(s_i, s_j)=L_1$ or $L_\infty$ for example
			- distance function $d$ is a metric iff
				- $d(x,y)=d(y,x),d(x,y)\geq 0$
				- $(d(x,y)=0$ iff $x=y)$ and $d(x,z)\leq d(x,y)+d(y,z)$
			- for a general metric $d$ the problem is not $\alpha$-approximable with $\alpha < 2$
			- for $d=L_2$ the problem is not $\alpha$-approximable with $\alpha < \sqrt 3 \approx 1.73$
			- for $d=L_1$ or $d=L_\infty$, the problem is not $\alpha$-approximable with $\alpha < 2$