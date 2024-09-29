---
tags:
  - edge_shape
---
- like [[Prewitt Operator]], Sobel relies on central differences, it does this by giving a greater weight to the central pixels:
	- $h_{hor}=\begin{bmatrix}-1&0&1\\-2&0&2\\-1&0&1\end{bmatrix}, h_{ver}=\begin{bmatrix}-1&-2&-1\\0&0&0\\1&2&1\end{bmatrix}$
	- can be an approximate as a derivative of a Gaussian
	- first applies [[Gaussian Filter]] to smooth then the derivation $\frac{d}{dx}(I*G)=I*\frac{dG}{dx}$
	![[Screenshot 2024-09-29 at 18.58.33.png|400]]