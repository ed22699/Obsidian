---
tags:
  - Lesson
  - suffix_trees
---
- input a test string $T$ (length $n$) and a pattern string $P$ (length $m$)
- goal is to find all the locations where $P$ matches in $T$
	- $P$ matches a location $i$ iff for all $0\leq j \leq m$ we have that $P[j]=T[i+j]$ (zero indexed)
![[Screenshot 2024-10-14 at 13.29.57.png|200]]
- a naive algorithm takes $O(nm)$ time
- we want a query time which depends only on $m$ and $occ$ (number of occurrences/matches)
- we also want $O(n)$ space and fast preprocessing time
	- example of an $O(n)$ time algorithm for this is KMP
# Suffix Trees
## Atomic Suffix Tree
![[Atomic suffix tree]]
## Compacted Suffix Tree
![[Compacted suffix tree]]
