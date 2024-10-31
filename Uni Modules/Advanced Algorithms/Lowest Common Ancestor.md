---
tags:
  - Lesson
  - lowest_common_ancestor
---
- preprocess a tree $T$ (with $n$ nodes) to answer lowest common ancestor queries
- after preprocessing the output to a query $LCA(i,j)$ is the lowest common ancestor of nodes $i$ and $j$
![[Screenshot 2024-10-31 at 13.16.15.png|400]]
- ideally, we would like $O(n)$ space, $O(n)$ prep time and $O(1)$ query time
## Solving LCAs using RMQs
![[Screenshot 2024-10-31 at 13.19.58.png|200]]
1. compute an Euler tour of T (a depth first search with repeats)
2. write down every node you visit and its depth
![[Screenshot 2024-10-31 at 13.20.19.png|300]]
- how do we find $LCA(i,j)$?
	- find $i$ and $j$ in $N$
	- compute $RMQ(i',j')$ ([[Range Minimum Queries]]) in $D$
>[!note]
any copy of $i$ and $j$ is fine to use

**Preprocessing Summary** - $O(n)$ space/prep time:
1. construct $N$ and $D$ from $T$ - $O(n)$
2. add a pointer from each node $i$ to some $N[i']=i$ - $O(n)$
3. preprocess $D$ for RMQs - $O(n)$ (using [[+-1 Range Minimum Query]])
**Query Summary** - $LCA(i,j)$ - $O(1)$:
1. find any $i'$ st. $N[i']=i$ - $O(1)$
2. find any $j'$ st. $N[j']=j$ - $O(1)$
3. compute $RMQ(i', j')$ in $D$ - $O(1)$ (using [[+-1 Range Minimum Query]])
4. $LCA(i,j)=N[RMQ(i',j')]$ - $O(1)$

to speed up we need to use $\pm$ range minimum queries as they take advantage of the fact that items in $D$ only ever increase or decrease by $1$
### $\pm$ Range Minimum Query
![[+-1 Range Minimum Query]]

