---
tags:
  - Lesson
  - 3D_reconstruction
---
## Epipolar Lines
- $\boldsymbol{p}_R^TE\boldsymbol{p}_L=0$
	- let $\boldsymbol{u}_L=E\boldsymbol{p}_L=\begin{bmatrix}u_{L1}\\u_{L2}\\u_{L3}\end{bmatrix}$
- $\boldsymbol{p}_R^T\boldsymbol{u}_L\Rightarrow x_Ru_{L1}+y_Ru_{L2}+fu_{L3}=0$
	- equation of epipolar line in right image
	![[Screenshot 2024-10-21 at 15.39.45.png|100]]
## Image Points and Pixels
- pixel values represent light intensity within small region of image plane, e.g. of size $s_x$x$s_y$ 
- $s_x$ size of the pixel in the $x$ direction
- pixel coordinates: $(\hat{x}, \hat{y})$
- principle point is where the $z$ axis cuts the image plane in a pinhole camera model
- can get most of this from the camera
![[Screenshot 2024-10-21 at 15.41.36.png|200]]
- $x=s_x(\hat{x}-\hat{o}_x)$
	- $x$ is the image coordinate
	- $\hat{x}$ is the location of the pixel in the $x$ direction
- $y=s_y(\hat{y}-\hat{o}_y)$
- $\boldsymbol{p}_R^TE\boldsymbol{p}_L=0 \Rightarrow \hat{\boldsymbol{p}}_R^TM_R^TEM_L\hat{\boldsymbol{p}}_L=0 \Rightarrow \hat{\boldsymbol{p}}_R^TF\hat{\boldsymbol{p}}_L=0$ 
	- $\boldsymbol{p}_L=\begin{bmatrix}x_L\\y_L\\f\end{bmatrix}=M_L\begin{bmatrix}\hat{x}_L\\\hat{y}_L\\f\end{bmatrix}=M_L\hat{\boldsymbol{p}}_L$
	- $F=M_R^TEM_L$ (fundamental matrix in pixel coordinates)
![[Screenshot 2024-10-21 at 15.54.26.png|300]]
- given set of correspondences, $i=1...N$, we can also estimate the fundamental matrix: $\hat{\boldsymbol{p}}_{Ri}^TF\hat{\boldsymbol{p}}_{Li}=0 \quad i=1...N$
