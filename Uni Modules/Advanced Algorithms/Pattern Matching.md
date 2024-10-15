---
tags:
  - Lesson
  - pattern_matching
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
![[Screenshot 2024-10-14 at 13.43.28.png|400]]
- suffix tree contains every suffix of $T$ as a root to leaf path
- every edge is labelled with a character from $T$
- no two edges leaving the same node have the same label
- each leaf corresponds to a suffix (so $n$ leaves)
**How to find a pattern**
- start at the root and walk down the tree
- matches occur at the leaves of the subtree
- we can decide whether $P$ matches somewhere in $O(m)$ time
>[!warning]
finding the correct child could take a while as there could be $n$ edges. Here we are assuming constant alphabet size. can remove this assumption with hashing

**How large is the atomic suffix tree?**
- there can be a lot of internal nodes
- atomic suffix tree can have $(\frac n2+1)^2$ nodes (very big)
## Compacted Suffix Tree
- replace each non-branching path with a single edge 
	- edges are now labelled with substrings rather than single characters 
![[Screenshot 2024-10-15 at 11.57.42.png|200]]
- there are $O(n)$ edges
	- there are at most $n$ leaves
	- every internal node has two or more children
- only store the end points, instead of storing "nas" we actually store $(4,6)$
**Compacted Suffix Tree** of T facts:
- a rooted tree with $n$ leaves
- every internal node has two or more children
- every edge is labelled with a substring
- no two edges leaving the same node have the same first character 
- each leaf is labelled with a location in $T$ 
- any root-to-leaf path spells out the corresponding suffix