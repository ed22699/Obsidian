---
tags:
  - Hashing
---
Construction is based on [[Weakly universal hashing]]
- indicator random variable $I_{x,y}=1$ iff $h(x)=h(y)$
# First concept
1. Insert everything into a hash table of size $m=n$ using a [[Weakly universal hashing]] function
2. check for collisions
3. repeat if necessary
## Average collisions
$$
\mathbb{E}(C)=\mathbb{E}(\sum_{x,y\in T, x<y}\mathbb{E}(I_{x,y})) \leq \sum_{x,y\in T, x<y}\frac{1}{m} = \begin{pmatrix}n\\2\end{pmatrix}\cdot \frac{1}{m}\leq\frac{n^{2}}{2m}\leq \frac{n}{2}
$$
- found with [[Linearity of expectation]], the definition of expectation and the idea that $\begin{pmatrix}n\\2\end{pmatrix}\leq \frac{n^{2}}{2}$
# Second Concept
1. insert everything into a hash table of size $m=n^{2}$ using a [[Weakly universal hashing]] function
2. check for collisions 
3. repeat if necessary
## Average Collisions
$$
\mathbb{E}(C)=\mathbb{E}(\sum_{x,y\in T,x<y}I_{x,y})=\sum_{x,y\in T, x<y}\mathbb{E}(I_{x,y})\leq\sum_{x,y\in T, x<y}\frac{1}{m}=\begin{pmatrix}n\\2\end{pmatrix}\cdot \frac{1}{m}\leq\frac{n^{2}}{2m}\leq\frac{1}{2}
$$
- found with [[Linearity of expectation]], the definition of expectation and the idea that $\begin{pmatrix}n\\2\end{pmatrix}\leq \frac{n^{2}}{2}$
## Expected Construction Time
- expected number of collisions: $\mathbb{E}(C)\leq\frac{1}{2}$



