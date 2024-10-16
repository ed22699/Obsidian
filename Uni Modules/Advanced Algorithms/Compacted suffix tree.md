---
tags:
  - suffix_trees
---
## Summary
- compacted suffix tree of a length $n$ text uses $O(n)$ space
- finding all matches of a pattern $P$ of length m takes $O(m+occ)$
- suffix trees can be built in $O(n)$ time (we only saw a $O(n^2)$ method, could build a [[Suffix Array]] as an alternative)
## Method
- replace each non-branching path with a single edge 
	- edges are now labelled with substrings rather than single characters 
![[Screenshot 2024-10-15 at 11.57.42.png|200]]
- there are $O(n)$ edges
	- there are at most $n$ leaves
	- every internal node has two or more children
- only store the end points, instead of storing "nas" we actually store $(4,6)$
- uses $O(n)$ space
**Compacted Suffix Tree** of T facts:
- a rooted tree with $n$ leaves
- every internal node has two or more children
- every edge is labelled with a substring
- no two edges leaving the same node have the same first character 
- each leaf is labelled with a location in $T$ 
- any root-to-leaf path spells out the corresponding suffix
### Issue
- compacted suffix tree doesn't always exist
![[Screenshot 2024-10-16 at 09.58.34.png|150]]
- above doesn't have $n$ leaves
**Solution**:
![[Screenshot 2024-10-16 at 09.59.27.png|150]]
- add a unique symbol to the end of the string
- above now has $n$ leaves
## Suffix Tree
This is a tree where a unique symbol is added to the end of $T$ in a compacted suffix tree to ensure there are $n$ leaves
![[Screenshot 2024-10-16 at 10.03.30.png|200]]
### Searching compacted suffix tree
- every child starts with a different character
- start at the root and walk down the tree (one character at a time)
	- matches occur at the leaves of the subtree
![[Screenshot 2024-10-16 at 10.13.42.png|400]]
- the size of subtrees is $O(occ)$ because it has $occ$ leaves and each internal node has at least two children
	- we can find all the matches in $O(m+occ)$ time by looking at the whole subtree
### Constructing a compacted suffix tree
#### Naive construction
inset suffix trees one at a time (longest first
- search for the new suffix in the partial suffix tree (as if you were pattern matching)
- add a new edge and leaf for the new suffix (may require you to break an edge in two)
	![[Screenshot 2024-10-16 at 10.20.08.png|300]]
	- ananas$ was stored as (1,7), however at this point is split and stored as:
		- ana as (1,3)
		- nas$ as (4,7)
- takes $O(n)$ time per suffix so $O(n^2)$ time in total
### Multiple text indexing
![[Screenshot 2024-10-16 at 10.28.42.png|400]]
- build a generalised suffix tree in $O(n_1+n_2)$ space
- using the linear time method (which we omitted), this takes $O(n_1+n_2)$ time
- finding all matches of a pattern $P$ of length $m$ still takes $O(m+occ)$ time
>[!note]
[[Suffix Array]] is much smaller than the suffix tree (in terms of constants)

- you can get a suffix array from a suffix tree by performing a depth-first search (in lexicographical order)
	- however this is quite a useless excise as you shouldn't have bothered with a suffix tree if you were going to use a suffix array 