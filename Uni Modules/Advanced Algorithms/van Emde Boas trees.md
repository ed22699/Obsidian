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
	- if $U=\{1,2,3,4,...100\cdot n\}$, you get $O(\log\log n)$ time and $O(n)$ space
	- if $U=\{1,2,3,4,...n^2\}$, you get $O(\log\log n)$ time and $O(n^2)$ space
	- if $U=\{1,2,3,4,...n^3\}$, you get $O(\log\log n)$ time and $O(n^3)$ space
#### Attempt 1: big array
make array the size of the universe and put a $1$ where element is present
- $A[i] = 1$ iff $i$ is in $S$
- add, delete and lookup all take $O(1)$ time
- predecessor and successor operations take $O(u)$ time
![[Screenshot 2024-10-06 at 14.44.13.png|300]]
#### Attempt 2: constant height tree (on top of a big array)
- split $A$ into $\sqrt u$ blocks each containing $\sqrt u$ bits
- for block $i$,, we build a data structure $B[i]$ which store elements from $\{1,2,3,...,\sqrt{u}\}$ 
	- $x$ is stored in $B[i]$ iff $(x+(i-1)\sqrt x)\in S$ 
- summary structure $C$ stores elements from $\{1,2,3,...,\sqrt{u}\}$
	- $i$ is stored in $C$ iff $B[i]$ is non-empty
- $C$ is called the summary of $A$
	- summary section is $1$ if any bit in the child block is $1$
- we build these blocks $\{B[1], B[2],...,B[\sqrt u]\}$ into $C$ through recursion 
	- each $B[i]$ has universe $\{1,2,3,...,\sqrt u\}$
	- recursively split each block into $\sqrt[\leftroot{-2}\uproot{2}4]{u}$ blocks, each associated with $\sqrt[\leftroot{-2}\uproot{2}4]{u}$ elements
	- eventually this will lead to an $O(\log\log u)$ time solution
![[Screenshot 2024-10-06 at 14.50.25.png|300]]
- lookup and add operations take $O(1)$ time
- delete, predecessor and successor take $O(\sqrt u)$ time
#### Attempt 3: Recursion
split the universe $U$ into $\sqrt u$ blocks, each associated with $\sqrt u$ elements
- to perform an $add(x)$:
	1. determine which $B[i]$ the element $x$ belongs in ($O(1)$)
	2. if $B[i]$ is empty, add $i$ to $C$ 
	3. add $x$ to $B[i]$ (adjusting the offset from the start of $B[i]$, and so we actually insert $x'$ where $x=(x' +(i - 1)\sqrt u)$)
	- makes up two recursive calls each recursive call could in turn make multiple recursive calls
- to perform $predecessor(x)$:
	1. determine which $B[i]$ the element $x$ belongs in 
	2. compute the predecessor of $x$ in $B[i]$ (suitably adjusting the offset from the start of $B[i]$)
	3. if $x$ has no predecessor in $B[i]$:
		- compute $j=predecessor(i)$ in $C$
		- compute the predecessor of $x$ in $B[j]$ (suitably adjusting the offset from the start of $B[j]$)
	- makes up three recursive calls each recursive call could in turn make multiple recursive calls
	- changes:
		2. if $x\geq$ them minimum in $B[i]$: return the predecessor of $x$ in $B[i]$
		3. if $x<$ the minimum in $B[i]$: 
			- compute $j=predecessor(i)$ in $C$
			- return the maximum in $B[j]$
	- now exactly one recursive call (excluding min/max)
- lookup, delete and successor cam also be defined in a similar recursive manner
#### van Emde Boas Trees
we can find the min/max quickly if we store them separately
![[Screenshot 2024-10-06 at 19.18.57.png|400]]
- each $B[i]$ and $C$ are also vEB trees each over the universe $\{1,2,3,...,\sqrt u \}$
- $B[i]$ also stores it's min/max elements separately
	- recovering the minimum or maximum in $B[i]$ (or $C$) takes $O(1)$ time
>[!note]
>minimum is not also stored in $B[i]$
- this allows us to avoid making multiple recursive calls when adding an element
- to perform $add(x)$:
	0. if $x<\min$ then swap $x$ and $\min$
	1. determine which $B[i]$ the element $x$ belongs in
	2. if $B[i]$ is empty, add $i$ to $C$ and set the min and max in $B[i]$ to $x$ (adjusting the offset)
	3. if $B[i]$ is not empty, add $x$ to $B[i]$
	4. update the max

#### Time Complexity
- let $T(u)$ be the time complexity of the add operation
	- we have that, $T(u)=T(\sqrt u)+O(1)$
	- using substitution and the master method you can show that $T(u)=O(\log\log u)$
- this holds for all the operations
- let $Z(u)$ be the space used by a vEB tree over a universe of size $u$
	- we have that, $Z(u)=(\sqrt u + 1)\cdot Z(\sqrt u)+O(1)$
	- simplified to $Z(u)=O(u)$ 
- the space can be improved to $O(n)$ using hashing (see y-fast trees)