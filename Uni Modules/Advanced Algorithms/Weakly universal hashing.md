---
tags:
  - Hashing
---
- A set $H$ of hash functions is weekly universal if for any two distinct keys $x,y \in U$ $P(h(x) = h(y)) \leq \frac{1}{m}$ where $h$ is chosen uniformly at random from $H$
	- randomness comes from the fact that $h$ is picked randomly
- Consider any $n$ fixed inputs to the hash table, pick $h$ uniformly at random from a weakly universal set $H$ of hash functions 
	- expected run-time per operation is $O(1)$ if $m \geq n$
## Example
- suppose $U=[u]$, i.e. the keys in the universe are integers $0$ to $u-1$
- let $p$ be any prime number bigger than $u$
- for $a,b \in [p]$, let
	- $h_{a,b}(x)=((ax+b)\mod p)\mod m$
	- $H_{p,m}=\{h_{a,b}|a \in \{1,...,p-1\},b \in \{0,...,p-1\}\}$
	- $ax+b$ is a linear transformation which spreads keys over $p$ when taken modulo $p$. This does not cause any collisions, only when taking modulo $m$ do we get collisions
# Longest Chain - weakly universal hashing
if $h$ is picked uniformly at random from a weakly universal set of hash functions then, over $m$ fixed inputs, $P($any chain has length $\geq 1 + \sqrt{2m}) \leq \frac{1}{2}$
- note the bad upper bound does not rule out the possibility that the tightest upper bound is indeed very small. However, the upper bound of $\frac{1}{2}$ is tight
## Proof
- for any two keys $x,y$ let indicator r.v. $I_{x,y}$ be $1$ iff $h(x)=h(y)$
- let r.v. $C$ be the total number of collisions: $C=\sum_{x,y \in T, x<y}I_{x,y}$ 
- using [[Linearity of expectation]] and $\mathbb{E}(I_{x,y})=\frac{1}{m}$ ($h$ is weakly universal)
$$
\mathbb{E}(C)=\mathbb{E}(\sum_{x,y\in T, x<y}I_{x,y})=\sum_{x,y\in T, x<y}\mathbb{E}(I_{x,y})=\begin{pmatrix}m\\2\end{pmatrix}\cdot \frac{1}{m}\leq \frac{m}{2}
$$
- by [[Markov's inequality]], $P(C\geq m)\leq \frac{\mathbb{E}(C)}{m}\leq \frac{1}{2}$
- let r.v. $L$ be the length of the longest chain $\to C \geq \begin{pmatrix}L\\2\end{pmatrix}$
- so, $P(\frac{(L-1)^{2}}{2}\geq m)\leq P(\begin{pmatrix}L\\2\end{pmatrix}\geq m)\leq P(C\geq m)\leq \frac{1}{2}$
	- rearranging we get $P(L\geq 1+\sqrt{2m})\leq \frac{1}{2}$