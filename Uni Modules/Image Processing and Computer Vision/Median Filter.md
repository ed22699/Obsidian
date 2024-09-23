---
tags:
  - Filtering
---
- returns the median value of pixels in a neighbourhood
- is non-linear
- removes salt and pepper noise
![[Screenshot 2024-09-23 at 10.18.46.png|400]]
## the algorithm
1. let $I$ be a monochrome image
2. let $Z$ define a neighbourhood of arbitrary shape
3. at each pixel location, $\boldsymbol{p}=(x,y)$, in $I$ 
	1. select the $n$ pixels in the Z-neighbourhood of $\boldsymbol{p}$ 
	2. sort the $n$ pixels in the neighbourhood of $\boldsymbol{p}$ by value into a list $L(j)$ for $j=1,...,n$
4. the output value at $\boldsymbol{p}$ is $L(m)$, where $m=[n/2]+1$
