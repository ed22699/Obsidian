---
tags:
  - suffix_arrays
---
- sort the suffixes lexicographically (order the strings as they would appear in the dictionary)
	- the symbols themselves must have an order
	- sort string based on the first symbol that differs
	- if tie then the shorter string is smaller
	- if the symbols don't have a natural order, we use their binary representation in memory
	![[Screenshot 2024-10-16 at 11.53.35.png|150]]
	![[Screenshot 2024-10-16 at 11.55.28.png|200]]
- suffix array is much smaller than the [[Compacted suffix tree]] (in terms of constants)
## Searching in the Suffix Array
- find an occurence of $P$ using a binary search
	- compare the midpoint value to that of the substring
	![[Screenshot 2024-10-16 at 11.59.43.png|300]]
	- takes $O(m)$ time to compare two strings, so $O(m\log n)$ total time
- method generalises to $O(m\log n+occ)$ time to find all $occ$ occurrences by continuing the binary search 
	- this can be further improved to $O(m+\log n+occ)$ time using LCP queries 
## DC3 Method
- $B_1$ contains indices with $i\mod 3=1$, $B_2$ contains indices with $i\mod 3=2$
- $R_1$ and $R_2$ are split into blocks of length 3
	- introduce a new filer symbol if final block is not of length 3
- $R$ is the concatenation of $R_1$ and $R_2$ 
	- number the blocks in $R$ in lexicographical order with $ being the smallest symbol
	- this can be done by sorting the blocks in $O(n)$ time using radix sort (assume the bit representation of each symbol uses $O(\log n)$ bits, which is common and realistic)
- $R'$ is the ordering of $R$
	- computer the suffix array of $R'$ (the positions of these ranked blocks), we do this via recursion (note $R'$ has length $\frac{2n}3$)
![[Screenshot 2024-10-26 at 11.17.45.png|400]]
- useful as if you take any two suffixes in $B_1 \cup B_2$ and find them in $R$ their order is given by the suffix array of $R'$
- relabel $R'$ to correspond to the initial positions in $T$
	![[Screenshot 2024-10-26 at 11.28.07.png|200]]
- to include the suffixes at $i\mod 3=0$ we note that suffix 0 is just y followed by suffix 1
	- each suffix $i\in B_0$ is represented by $(T[i],r)$ where $r$ is the rank of suffix $(i+1)$
		- we can sort $B_0$ in $O(n)$ time using radix sort
	- we merge the two lists like a merge sort. It takes $O(1)$ time to decide on a smaller item
		- $6 = a+7 \quad (a,4)$, $1=a+2\quad (a,3)$ 
	- overall this merging phase takes $O(n)$ time because processing each suffix takes $O(1)$ time
- suppose $T(n)$ is the running time, we have: $T(n)=T(2n/3)+O(n)$, this is the recursion to construct a suffix array of size $2n/3$ and the radix sorting and merging
	- solving this recurrence gives $T(n)\in O(n)$