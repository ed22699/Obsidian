---
tags:
  - lowest_common_ancestor
---
A special case of [[Range Minimum Queries]] where $D[i+1]=D[i]\pm 1$

- preprocess an integer array $A$ (length $n$) to answer range minimum queries where for all $k$, we have $A[k+1]=A[k]\pm 1$
- after preprocessing, a range minimum query is given by $RMQ(i,j)$ the output is the location of the smallest element in $A[i,j]$ (in a tie, report the leftmost)
- **Key idea**: replace $A$ with a smaller, 'low resolution' array $H$ and many small arrays $L_0, L_1, L_2,...$ for the details
	![[Screenshot 2024-10-31 at 13.38.23.png|300]]
	- $\tilde n = \frac{2n}{\log n}$
	- preprocess the array $H$ (which has length $\tilde n)
