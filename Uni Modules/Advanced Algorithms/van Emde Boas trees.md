---
tags:
  - Lesson
  - van_emde_boas_trees
---
- dynamic dictionary data structure we store (key, value)-pairs such that for any key there is at most one pair (key, value) in the dictionary
- three operations:
	- $add(x,v)$ - add the pair $(x,v)$ where $x\in U$
	- $lookup(x)$ - return $v$ if $(x,v)$ is in dictionary, $NULL$ otherwise
	- $delete(x)$ - remove pair $(x,v)$
- looking at hashing, the main issues are randomness, amortisation and inflexibility
## Supporting more operations
say we want our data structure to support:
- $predecessor(k)$ - returns the unique element $(x,v)$ in the dictionary with the largest key, $x$ s.t. $x \leq k$
- $successor(k)$ - returns the unique element $(x,v)$ in the dictionary with the smallest key, $x$ s.t. $x\geq k$
hashing is not suited to these operations. Other options:
- use self-balancing binary tree
	- 2-3-4 tree
	![[Screenshot 2024-10-06 at 14.32.53.png|150]]
	- red-black tree
	![[Screenshot 2024-10-06 at 14.33.23.png|150]]
	- AVL tree
- all three
	- support all these operations, each in $O(\log n)$ worst case time and $O(n)$ space where $n$ is the number of elements stored
	- are deterministic
### Van Emde Boas Trees
- Van Emde Boas Trees store a set $S$ of integer keys from a universe $U=\{1,2,3,4,...,u\}$
>[!note]
do not store any data (values) with the integers (keys), however, it is straightforward to extend vEB trees to store (key, value) pairs

- all operations take $O(\log\log u)$ worst case time and the space used is $O(u)$
- deterministic data structure
>[!todo]
>look up deterministic data structure effect

#### Attempt 1: big array
make array the size of the universe and put a $1$ where element is present
- $A[i] = 1$ iff $i$ is in $S$
- add, delete and lookup all take $O(1)$ time
- predecessor and successor operations take $O(u)$ time
![[Screenshot 2024-10-06 at 14.44.13.png|300]]
#### Attempt 2: constant height tree (on top of a big array)
- split $A$ into $\sqrt u$ blocks each containing $\sqrt u$ bits
- $C$ is called the summary of $A$
	- summary section is $1$ if any bit in the child block is $1$
![[Screenshot 2024-10-06 at 14.50.25.png|300]]
- lookup and add operations take $O(1)$ time