---
tags:
  - segmentation
---
**Homogeneity function H**:
- $H($Region A$)=1$ (homogeneous)
- $H($Region B$)=0$ (inhomogeneous)
![[Screenshot 2024-10-01 at 12.11.26.png|150]]
## Idea
- iteratively decompose an image into regions of a maximally sized selected shape (e.g. rectangle) that do not satisfy a homogeneity condition (split step)
- merge regions that together satisfy a homogeneity condition (merge step)
- using quadtrees, the results of a split and merge tend to be blocks
	- can have an adaptive homogeneity condition that, for instance, changes depending on the region size
	- e.g. $H(R_i)=1$ if at least 80% of the pixels in $R_i$ have the property $|z_j-m_i|<2\sigma$, set all the pixels in $R_i$ to value $m_i$
		- $z_j$ is the grey level of the $j^{th}$ pixel in $R_i$
		- $m_i$ is the mean grey level of the region 
		- $\sigma_i$ is the standard deviation of the grey levels in $R_i$
## Algorithm
1. Start with $R_0$ that represents the entire image
2. if $H(R_i)=0$ (inhomogeneous) then 
	1. split area into 4 blocks (quadtree splitting)
	2. process each area with step 2
3. merge all subregions that pairwise satisfy $H(R_i \cap R_j)=1$ (homogenous)
![[Screenshot 2024-10-01 at 12.15.36.png|300]] ![[Screenshot 2024-10-01 at 12.16.22.png|90]]


