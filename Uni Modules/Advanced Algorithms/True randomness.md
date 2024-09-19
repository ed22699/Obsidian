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


