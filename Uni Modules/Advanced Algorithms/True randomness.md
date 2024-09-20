---
tags:
  - Hashing
---
- Consider any $n$ fixed inputs to the hash table (of size $m$) i.e. any sequence of $n$ add/lookup/delete operations
- Pick $h$ uniformly at random from the set of all functions $U \to [m]$ 
- expected run-time per operation is $O(1 + \frac{n}{m})$, or $O(1)$ if $m \geq n$
## Proof
let indicator r.v. $I_{x,y}$ be $1$ iff $h(x) = h(y)$ 
- $P(h(x) = h(y))=\frac{1}{m}$
- $\mathbb{E}(I_{x,y})=\frac{1}{m}$
Let $N_{x}$ be the number of keys stored in $T$ that are hashed to $h(x)$
- $N_{x}=\sum_{y \in T}I_{x,y}$ 
- $\mathbb{E}(N_{x})=\mathbb{E}(\sum_{y \in T}I_{x,y}) = \sum_{y \in T}\mathbb{E}(I_{x,y}) = n \cdot \frac{1}{m} = \frac{n}{m}$


# Longest Chain - true randomness
if $h$ is selected uniformly at random from all functions $U \to [m]$ then over $m$ fixed inputs $P($any chain has length $\geq 3\log m)\leq \frac{1}{m}$
- note in lemma we insert $m$ keys ($n=m$)
## Proof
equivalent to throwing $m$ balls into $m$ bins, the probability of having a bin with at least $3 \log m$ balls is at most $\frac{1}{m}$
![[Screenshot 2024-09-19 at 15.36.50.png|400]]
- let $X_{1}$ be the number of balls in the first bin, choose any $k$ of the $m$ balls the probability that all of these $k$ balls go into the first bin is $\frac{1}{m^{k}}$
- [[Union bound]] gives us $P(X_{1} \geq k) \leq \begin{pmatrix} m\\k \end{pmatrix} \cdot \frac{1}{m^{k}} \leq \frac{1}{k!}$ 
	- note $\begin{pmatrix} m\\k \end{pmatrix} = \frac{m!}{k!(m-k)!} = \frac{m \cdot (m-1) \cdot (m-2) \cdot ... \cdot (m-k+1) \cdot (m-k)!}{k!(m-k)!} = \frac{m \cdot (m-1) \cdot (m-2) \cdot ... \cdot (m-k+1)}{k!}$ 
	$\leq \frac{m\cdot m \cdot m \cdot ... \cdot m}{k!} \leq \frac{m^{k}}{{k!}}$
	
- [[Union bound]] again gives us $P($at least one bin receives at least $k$ balls$)\leq m \cdot P(X_{1}\geq k)\leq \frac{m}{k!}$
- where $k=3\log m$ we observe $\frac{m}{k!}\leq \frac{1}{m}$ for $m \geq 2$ 
	- note $k! > 2^{k-1}$ 
	- $2^{(3\log m-1)} \geq 2^{2\log m}=m^{2}$ 
	
	

