---
tags:
  - pattern_matching
---
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