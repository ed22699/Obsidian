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
