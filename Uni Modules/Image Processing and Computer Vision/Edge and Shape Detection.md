---
tags:
  - Lesson
  - edge_shape
---
# Edges
- shapes are more informative than individual pixel values
- edges highlight the contour of shapes, are used to identify objects
	- for segmentation: finding object boundaries
	- for recognition: extracting patterns
	- for motion analysis: reliable tracking regions
- strategy - determine a 'measure of change' in the pixel's neighbourhood
	- first derivatives in 2D space $\to$ image gradient:
		- $\nabla f(x,y)=\frac{df}{dx} \hat{x}+\frac{df}{dy}\hat{y}$
		- image gradient is a vector variable
		- direction $\psi$ of the maximum growth of the function ($\psi=\tan^{-1}(\frac{df/dy}{df/dx})$) is perpendicular to the edge direction $\phi$ ($\phi=\psi-\frac{\pi}{2}$)
		- magnitude of the growth $|\nabla f(x,y)|=\sqrt{(\frac{df}{dt})^{2}+(\frac{df}{dy})^{2}}$
		![[Screenshot 2024-09-29 at 18.33.20.png|200]]
		- using $h_{x}=\begin{bmatrix}-1&0&1\\-1&0&1\\-1&0&1\end{bmatrix}$ and $h_{y}=\begin{bmatrix}-1&-1&-1\\0&0&0\\1&1&1\end{bmatrix}$ as filters
		![[Screenshot 2024-09-29 at 18.37.42.png|500]]
	 ![[Prewitt Operator]]	
	 ![[Sobel Operator]]
# Shape Detection
![[Hough Transform]]
## Circle Detection Algorithm
1. for any pixel satisfying $|G(x,y)|>T_{s}$, increment all elements satisfying the two simultaneous equations
$$
\forall r, \begin{cases}x_{0}=x\pm r\cos\angle G \\y_{0}=y\pm r\sin \angle G\end{cases}
$$
$$
H(x_{0}, y_{0}, r)=H(x_{0}, y_{0},r)+1
$$
2. in the parameter space, any element $H(x_{0},y_{0},r)>T_{h}$ represents a circle with radius $r$ located at $(x_{0}, y_{0})$ in the range 