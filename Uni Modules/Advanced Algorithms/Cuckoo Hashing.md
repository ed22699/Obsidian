---
tags:
  - Hashing
---
- collisions are fixed by bucketing rather than chaining
- we require that we can recover any key from its bucket in $O(s)$ time where $s$ is the number of keys in the bucket
- locating the bucket containing a given key takes $O(1)$ time
- Hash table $T$ of size $m\geq n$
![[Screenshot 2024-09-30 at 11.27.46.png|300]]
- if our construction has the property that for any two keys $x,y\in U$ (with $x\neq y$) the probability that $x$ and $y$ are in the same bucket is $O(\frac{1}{m})$ 
- for any $n$ operations, the expected run-time is $O(1)$ per operation
# Cuckoo hashing scheme
- every lookup and every delete takes $O(1)$ worst-case time
- the space is $O(n)$ where $n$ is the number of keys stored
- an insert takes [[amortised expected]] $O(1)$ time
In Cuckoo hashing there is a single hash table but two hash functions: $h_1$ and $h_2$
- each key in the table is either stored at position $h_1(x)$ or $h_2(x)$
>[!important]
never store multiple keys at the same position

## Inserts
![[Screenshot 2024-09-30 at 11.38.46.png|400]]
1. attempt to put $x$ in position $h_1(x)$ (if that position is empty, stop)
2. let $y$ be the key currently in position $h_1(x)$, evict key $y$ and replace it with key $x$
3. let $pos$ be the other position $y$ is allowed to be in, i.e. $pos=h_2(y)$ if $h_1(x)=h_1(y)$ and $pos=h_1(y)$ otherwise
4. attempt to put $y$ in position $pos$ (if that position is empty, stop)
5. let $z$ be the key currently in position $pos$, evict key $z$ and replace it with key $y$ and so on