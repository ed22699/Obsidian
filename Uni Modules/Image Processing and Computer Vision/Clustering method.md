---
tags:
  - segmentation
---
![[Screenshot 2024-10-01 at 12.34.55.png|300]]
- if we knew the cluster centres, we could allocate points to groups by assigning each to its closest centre
- if we knew the group memberships, we could get the centres by computing the mean per group
![[Screenshot 2024-10-01 at 12.34.23.png|400]]
## K-means
**Aim**: Choose three "centres" as the representative intensities, and label every pixel according to which of these centres it is nearest to
- best cluster centres are those that minimise SSD between all points and their nearest cluster centre $\mu_j$
$$
\Theta(clusters,data)=\sum_{j\in clusters}[\sum_{i\in j^{th}cluster}||\boldsymbol{x}_i-\boldsymbol{\mu}_j||^{2}]
$$
- is an iterative clustering algorithm
	- pick $K$ random points as cluster centres (means)
	- iterate:
		- assign data instances to closest mean
		- assign each mean to the average of its assigned points
		- stop when no point's assignment changes
	![[Screenshot 2024-10-01 at 13.25.09.png|200]]
- attempts to find a configuration $\mu_1,...,\mu_K$ that minimises within-cluster scatter: total squared distance between point $x_i$ and centroid $\mu_j$ in the $j^{th}$ cluster
- equivalent to maximising the between-cluster scatter (total squared distance between each cluster centroid and the global centroid of all points)
1. algorithm terminates
2. finds a local optimum from which no further improvement is possible by making local changes
3. it does not necessarily find a global optimum
- can go wrong
![[Screenshot 2024-10-01 at 13.30.14.png|150]]
**Pros**:
- simple, fast to compute
- converges to local minimum of within-cluster squared error
**Cons**:
- setting K?
- sensitive to initial centres
- sensitive to outliers
![[Screenshot 2024-10-01 at 13.32.36.png|200]]
- detects spherical clusters
![[Screenshot 2024-10-01 at 13.32.11.png|200]]
## Feature space
we can group pixels in different ways with different feature spaces
- grouping pixels based on intensity similarity
- grouping pixels based on colour similarity
- grouping pixels based on intensity and position similarity