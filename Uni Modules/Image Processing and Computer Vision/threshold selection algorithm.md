---
tags:
  - segmentation
---
1. select an initial estimate for the threshold $T$ 
2. segment the image using $T$
	- this will produce two groups of pixels: 
		- $G_1$ consisting of all the pixels with grey levels $>T$
		- $G_2$ consisting of pixels with grey values $\leq T$
3. compute the average grey level values $m_1$ and $m_2$ for the pixels in regions $G_1$ ad $G_2$
4. compute a new threshold value: $T=(m_1+m_2)/2$ 
5. repeat steps 2-4 until convergence