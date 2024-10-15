---
tags:
  - Hashing
---
1. insert everything into a hash table $T$, of size $n$ using a weakly universal hash function, $h$, but don't use chaining
- let $n_{i}$ be the number of items in $T[i]$
2. the $n_{i}$ items in $T[i]$ are inserted into another hash table $T_{i}$ of size $n_{i}^{2}$ using another weakly universal hash function denoted $h_{i}$ (one for each $i$) 
3. immediately repeat a step if either
	1. $T$ has more than $n$ collisions
	2. some $T_{i}$ has a collision
![[Screenshot 2024-09-30 at 11.00.59.png|150]]
- lookup time is always $O(1)$
1. compute $i=h(x)$ ($x$ is the key)
2. compute $j=h_{i}(x)$
3. the item is in $T_{i}[j]$
## Space Usage
- size of $T$ is $O(n)$
- size of $T_{i}$ is $O(n_{i}^{2})$
- storing $h_{i}$ uses $O(1)$ space
- total space:
$$
O(n)+\sum_{i}O(n_{i}^{2})=O(n)+O(\sum_i n_i^2)= O(n)
$$
- $\sum_i n_i^2$ size?
	- are $\begin{pmatrix}n_i\\2\end{pmatrix}$ collisions in $T[i]$, so there are $\sum_i \begin{pmatrix}n_i\\2\end{pmatrix}$ collisions in $T$
	- there are at most $n$ collisions in $T$: $\sum_i \frac{n_i^2}{4}\leq\sum_i\begin{pmatrix}n_i\\2\end{pmatrix}\leq n$ or $\sum_i n_i^2 \leq 4n$
## Expected Construction Time
- expected construction time for $T$ is $O(n)$
- expected construction time for each $T_i$ is $O(n_i^2)$
- so overall expected construction time is:
	- $\mathbb{E}($construction time$)=\mathbb{E}($construction time of $T+\sum_i$construction time of $T_i)$
	- $=\mathbb{E}($construction time of T$)+\sum_i \mathbb{E}($construction time of $T_i)$
	- $O(n)+\sum_i O(n_i^2)=O(n)+O(\sum_i n_i^2)=O(n)$
## Question
is n the number of inputs if so how can the number of collisions ever be greater?