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
	