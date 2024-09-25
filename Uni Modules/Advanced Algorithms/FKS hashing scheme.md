---
tags:
  - Hashing
---
Construction is based on [[Weakly universal hashing]]
# First concept
1. Insert everything into a hash table of size $m=n$ using a [[Weakly universal hashing]] function
2. check for collisions
3. repeat if necessary
## Average collisions
$$
\mathbb{E}(C)=\mathbb{E}(\sum_{x,y\in T, x<y}\mathbb{E}(I_{x,y})) \leq \sum_{x,y\in T, x<y}\frac{1}{m} = \begin{pmatrix}n\\2\end{pmatrix}\cdot \frac{1}{m}\leq\frac{n^{2}}{2m}\leq \frac{n}{2}
$$
- found with [[Linearity of expectation]], the definition of expectation and the idea that $\begin{pmatrix}n\\2\end{pmatrix}\leq \frac{n^{2}}{2}$

