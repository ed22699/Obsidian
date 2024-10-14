---
tags:
  - Lesson
  - orthogonal_range_searching
---
- a 2D range searching data structure which stores $n$ distinct $(x,y)$-pairs and supports:
	- $lookup(x_1,x_2,y_1,y_2)$ - returns every point in the rectangle $[x_1:x_2]$x$[y_1:y_2]$ i.e. every $(x,y)$ with $x_1 \leq x \leq x_2$ and $y_1\leq y\leq y_2$
	![[Screenshot 2024-10-14 at 10.19.40.png|200]]
	![[Screenshot 2024-10-14 at 10.21.42.png|150]]
- for $d=1$, $lookup(x_1,x_2)$ returns every point with $x_1\leq x \leq x_2$
	- **Solution 1** (binary search): $O(\log n +k)$ lookup time
		1. build sorted array containing the $x$-coordinates in $O(n\log n)$ preprocessing time and $O(n)$ space
		2. find successor of $x_1$ by binary search then walk right while $x \leq x_2$, takes $O(\log n+k)$ time ($k$ is the number of points reported)
		![[Screenshot 2024-10-14 at 10.32.24.png|200]]
	- **Solution 2** (balanced tree): $O(\log n+k)$ lookup time
		1. **Construct tree**: find the point in the middle and recurse on each half (if tie, pick left), $O(n \log n)$ time ($O(n)$ if points are sorted), $O(n)$ space, $O(\log n)$ depth
			![[Screenshot 2024-10-14 at 10.36.32.png|200]]
		2. **Search Tree**: $O(\log n+k)$ 
			1. find successor of $x_1$ (tree traversal), $O(\log n)$ time
			2. find predecessor of $x_2$ (tree traversal), $O(\log n)$ time
			3. look at any node on path, check its off-path edges (choose all or nothing) and add those which are in range, $O(\log n+k)$ time ($k$ is the number of points reported)
				![[Screenshot 2024-10-14 at 10.47.06.png|300]]
				
- for $d=2$, $lookup(x_1,x_2,y_1,y_2)$ returns every point with $x_1\leq x \leq x_2$ and $y_1\leq y \leq y_2$ 
	- **Solution 1**: $O(\log n+k_x+k_y)$
		1. find all points with $x_1\leq x \leq x_2$, $O(\log n+k_x)$ time
		2. find all points with $y_1\leq y \leq y_2$, $O(\log n+k_y)$ time
		3. find all the points in both lists, $O(\log n +k_x+k_y)$
	- **Solution 2**: $O(\log^2n+k)$ lookup time
		1. build balanced binary tree using $x$-coordinates, $O(\log n)$ time
		2. follow paths to $x_1$ and $x_2$ discarding off-path subtrees where the $x$ coordinates are too large or small, $O(\log n)$ time
		3. filter the in range subtrees by $y$-coordinate by building a 1D range searching structure on all these valid trees, $O(\log n +k')$ time (where $k'$ is the size of the subtree) for each tree, with $O(\log n)$ lookups, so $O(\log^2 n+k)$ time
		![[Screenshot 2024-10-14 at 10.57.13.png|300]]
		- as the tree has depth $O(\log n)$ and the sizes of the arrays add up to $n$, the total space used is $O(n\log n)$	
		- preprocessing time $O(n\log n)$ 
	- **Solution 2 (improved)**: $O(\log n +k)$ lookup time
		- when we do a 2D look-up we do $O(\log n)$ 1D lookups, all with the same $y_1$ and $y_2$ 
		- slow part is finding the successor of $y_1$, if you knew where this point was a 1D lookup would only take $O(k')$ time
			- arrays of points at the children partition the array of the parent
				- The child arrays are sorted by $y$ coordinate (but have been partitioned by $x$ coordinate)
			- consider a point in the parent array, we add a link to its successor in both child arrays (doing this at every point during preprocessing)
			- if we know where the successor of $y_1$ is in the parent, we can find the successor in either child in $O(1)$ time (adding these links doesn't increase the space or the prep time)
				![[Screenshot 2024-10-14 at 11.28.17.png|300]]
		1. follow the paths to $x_1$ and $x_2$ (updating the successor to $y_1$ as you go)
		2. discard off-path subtrees where the $x$ coordinates are too large or too small
		3. for each off-path subtree where the $x$ coordinates are in range use the 1D range structure for that subtree to filter the $y$ coordinates
- for $d=3$, $lookup(x_1,x_2,y_1,y_2,z_1,z_2)$ returns every point with $x_1\leq x \leq x_2$, $y_1\leq y \leq y_2$ and $z_1\leq z \leq z_2$
