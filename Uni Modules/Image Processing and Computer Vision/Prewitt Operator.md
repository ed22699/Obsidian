---
tags:
  - edge_shape
---
Central difference $\frac{df}{dx}\approx \frac{f(x+1)-f(x-1)}{2}$
- mask $\begin{bmatrix}-1&0&1\end{bmatrix}$ is very sensitive to noise, solution: smooth in the perpendicular direction
- for a 3x3 mask, $\nabla f$ is estimated in 8 directions:
	- $h_{hor}=\begin{bmatrix}1&1&1\\0&0&0\\-1&-1&-1\end{bmatrix}, h_{dia}=\begin{bmatrix}0&1&1\\-1&0&1\\-1&-1&0\end{bmatrix},...$ 
	![[Screenshot 2024-09-29 at 18.49.45.png|300]]
	![[Screenshot 2024-09-29 at 18.50.22.png|100]]$\to$ ![[Screenshot 2024-09-29 at 18.50.59.png|100]]
	