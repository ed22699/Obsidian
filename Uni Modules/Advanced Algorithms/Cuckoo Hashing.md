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
- if cyclic, give up and rehash the whole table, i.e. empty the table, pick two new hash functions and reinsert every key
## Rehashing
- if we fail to insert a new key $x$ (i.e. we still have an "evicted" key after moving around keys $n$ times) then we declare the table "rubbish" and rehash
suppose that the table contains the $k$ keys $x_1,...,x_k$ at the time when we fail to insert key $x$
1. randomly pick two new hash functions $h_1$ and $h_2$
2. build a new empty hash table of the same size
3. reinsert the keys $x_1,...,x_k$ and then $x$, one by on, using the normal add operation
4. if we fail while rehashing, start from the beginning
### Assumptions
- $h_1$ and $h_2$ are independent (reasonable) 
- $h_1$ and $h_2$ are truly random (unreasonable)
- computing the value of $h_1(x)$ and $h_2(x)$ takes $O(1)$ worst-case time (questionable)
- there are at most $n$ keys in the hash table at any time (not assumption, true)
### Graph
![[Screenshot 2024-09-30 at 11.53.24.png|100]]
Cuckoo graph:
- a vertex for each position of the table
- for each key $x$ there is an undirected edge between $h_1(x)$ and $h_2(x)$
- number of moves performed while adding a key is the length of the corresponding path in the cuckoo graph
	- inserting key $x_6$ creates a cycle (cycles are dangerous)
	- when key $x_7$ is inserted where does it go? (6 keys but only 5 spaces)
	- keys would be moved around in an infinite loop but we stop and rehash after $n$ moves
- inserting a key into a cycle **always** causes a rehash
	- only way a rehash can happen
#### Paths in the cuckoo graph
for any positions $i$ and $j$, and any constant $c>1$, if $m\geq 2cn$ then the probability that there exists a shortest path in the cuckoo graph from $i$ to $j$ with length $\ell \geq 1$, is at most $\frac{1}{c^\ell \cdot m}$ 
- probability of a shortest path of length 4 is at most $\frac{1}{16m}$ 
- likelihood of a path is:
	- if a path exists from $i$ to $j$, there must be a shortest path (from $i$ to $j$)
	- the probability of a path from $i$ to $j$ existing is at most $\sum_{\ell=1}^{\infty}\frac{1}{c^{\ell}\cdot m}=\frac 1 m \sum_{\ell=1}^{\infty}\frac{1}{c^{\ell}}=\frac{1}{m\cdot (c-1)}= \frac 1 m$
	- so a path from $i$ to $j$ is rather unlikely to exist
	![[Screenshot 2024-09-30 at 12.07.30.png|400]]
## Buckets
![[Screenshot 2024-09-30 at 12.16.06.png|100]]
- we say that two keys $x,y$ are in the same bucket iff there is a path between $h_1(x)$ and $h_1(y)$ in the cuckoo graph
- for two distinct keys $x,y$, the probability that they are in the same bucket is at most
$$
\sum_{\ell=1}^{\infty}\frac{4}{c^{\ell}\cdot m}=\frac 4 m \cdot \sum_{\ell=1}^{\infty}\frac{1}{c^{\ell}}= \frac{4}{m(c-1)}=O(\frac 1 m)
$$
- where $c>1$ is a constant and using the lemma from paths in the cuckoo graph
- the time for an operation on $x$ is bounded by the number of items in the bucket meaning an expected time per operation of $O(1)$ (assuming that $m\geq 2cn$ and there are no cycles)
### Rehashing
- we would expect there to be cycles every now and then, causing a rehash
- how often?
	- consider inserting $n$ keys into the table
	- a cycle is a path from a vertex $i$ back to itself
	- probability that a position $i$ is involved in a cycle is at most: $\sum_{\ell=1}^{\infty}\frac{1}{c^{\ell}\cdot m}= \frac{1}{m(c-1)}$
	- probability that there is at least one cycle is at most: $m\cdot \frac{1}{m(c-1)}=\frac{1}{c-1}$
	- if we set $c=3$, the probability is at most $\frac 1 2$ that a cycle occurs during $n$ insertions (probability of two rehashes is $\frac 1 4$ and so on)
	- expected number of rehashes during $n$ insertions is at most $\sum_{i=1}^{\infty}(\frac 1 2)^i = 1$
- if the expected time for one rehash is $O(n)$ then the expected time for all rehashes is also $O(n)$ so [[amortised expected]] time for the rehashes over the $n$ insertions is $O(1)$ per insertion
- why expected time per rehash $O(n)$?
	- pick a new random $h_1$ and $h_2$ and construct the cuckoo graph using the at most $n$ keys
	- check for a cycle in the graph in $O(n)$ time (start again if found)
	- if there is no cycle, insert all the elements this takes $O(n)$ time in expectation
#### Assumptions
- we have assumed true randomness, this is not realistic
- we have seen that weakly universal hash families are realistic 
- we can define a stronger hash families with $k$-wise independence 
	- a set $H$ of hash functions in $k$-wise independent if for any $k$ distinct keys $x_1,x_2,...,x_k \in U$ and $k$ values $v_1,v_2,...,v_k \in \{0,1,2,...,m-1\}$,
	$$
	P(\cap_i h(x_i)=v_i)=\frac{1}{m^{k}}
	$$
	- where $h$ is picked uniformly at random from $H$
- it is feasible to construct a ($\log n$)-wise independent family of hash functions such that $h(x)$ can be computed in $O(1)$ time
- by changing the cuckoo hashing algorithm to perform a rehash after $\log n$ moves it can be shown that the results still hold
		
		