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