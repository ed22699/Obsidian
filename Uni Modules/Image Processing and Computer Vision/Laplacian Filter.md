---
tags:
  - Filtering
---

- Laplacian Filter: $\begin{bmatrix}0&1&0\\1&-4&1\\0&1&0\end{bmatrix}$
	- isotropic
	- one of the simplest filters for sharpening
- Laplacian defined as: $\nabla^{2}f=\frac{d^{2}f}{d^{2}x}+\frac{d^{2}f}{d^{2}y}$
	- partial $1^{st}$ order derivative in the $x$ direction is $\frac{d^{2}f}{d^{2}x}=f(x+1,y)+f(x-1,y)-2f(x,y)$
	- and in the $y$ direction is $\frac{d^{2}f}{d^{2}y}=f(x,y+1)+f(x,y-1)-2f(x,y)$
	- so Laplacian can be $\nabla^{2}f=[f(x+1,y)+f(x-1,y)+f(x,y+1)+f(x,y-1)]-4f(x,y)$
- is a derivative operator
	- highlights grey-level discontinuities in an image
	- de-emphasises regions with slowly varying grey-levels
	- very sensitive to noise as taking derivatives increases noise