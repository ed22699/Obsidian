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