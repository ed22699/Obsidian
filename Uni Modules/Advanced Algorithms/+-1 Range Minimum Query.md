---
tags:
  - lowest_common_ancestor
---
A special case of [[Range Minimum Queries]] where $D[i+1]=D[i]\pm 1$
### Low resolution RMQ
- preprocess an integer array $A$ (length $n$) to answer range minimum queries where for all $k$, we have $A[k+1]=A[k]\pm 1$
- after preprocessing, a range minimum query is given by $RMQ(i,j)$ the output is the location of the smallest element in $A[i,j]$ (in a tie, report the leftmost)
- **Key idea**: replace $A$ with a smaller, 'low resolution' array $H$ and many small arrays $L_0, L_1, L_2,...$ for the details
	![[Screenshot 2024-10-31 at 13.38.23.png|300]]
	- $\tilde n = \frac{2n}{\log n}$
	- preprocess the array $H$ (which has length $\tilde n$)
	- preprocess each array $L_i$ (which has length $\frac{(\log n)}2$)
	- as there are $O(\frac n {\log n})$ $L_i$ arrays, we have $O(n\log \log n)$ total space/prep time
### Counting $\pm$ RMQ arrays
- we say that $L_x$ is equivalent to $L_y$ iff for all $(i,j):RMQ_x(i,j)=RMQ_y(i,j)$ (these are the locations of the minimum)
![[Screenshot 2024-10-31 at 13.44.33.png|300]]
- $d_x$ is the decimal equivalent of the binary where a $-$ is a $0$ and a $+$ is a $1$
- $L_x$ is equivalent to $L_y$ iff $d_x=d_y$
- we can precompute $d_x$ for each $L_x$ in $O(|L_x|)=O(\log n)$ time
- $d$ contains $\frac{(\log n)}2-1$ bits so at most $2^{\frac {(\log n)}2}=(2^{\log n})^{1/2} \leq \sqrt n$ many different values of $d$
- for each value of $d$ we store $RMQ(i,j)$ for all $i,j$ this requires $O(\sqrt n \log^2 n)=O(n)$ total space and prep time
**Precompute**:
- precompute the value of $d_x$ for each $L_x$ in $O(n)$ total space and prep time
- precompute all the RMQ answers for every value $0\leq d\leq \sqrt n$ into a table in $O(n)$ total space and prep time 
**Perform a query within some $L_x$** - $O(1)$:
- look up $d_x$
- find the row $d_x$ in the table
- find the entry giving $RMQ_x(i,j)$ 