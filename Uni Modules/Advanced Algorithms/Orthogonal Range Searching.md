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
- for $d=2$, $lookup(x_1,x_2,y_1,y_2)$ returns every point with $x_1\leq x \leq x_2$ and $y_1\leq y \leq y_2$ 
- for $d=3$, $lookup(x_1,x_2,y_1,y_2,z_1,z_2)$ returns every point with $x_1\leq x \leq x_2$, $y_1\leq y \leq y_2$ and $z_1\leq z \leq z_2$
