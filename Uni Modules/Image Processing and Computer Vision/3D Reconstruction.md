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
- given set of correspondences, $i=1...N$, we can also estimate the fundamental matrix: $\hat{\boldsymbol{p}}_{Ri}^TF\hat{\boldsymbol{p}}_{Li}=0 \quad i=1...N \Rightarrow A\boldsymbol{v}=0$
	- $A$ - $N$x$9$ matrix defined by correspondence vectors $\hat{\boldsymbol{p}}_{Li}$ and $\hat{\boldsymbol{p}}_Ri$
	- $\boldsymbol{v}$ - components of $F$
	- solve for $\boldsymbol{v}$ using singular value decomposition
## 3D Reconstruction
![[Screenshot 2024-10-21 at 17.21.26.png|200]]
- you take a ray from the left camera and a ray from the right camera and find the point where they cross
	- **problem**: relies on them being ridiculously accurate to cross
	- instead find an approximation
- assume that they do not cross, we find the shortest line between the two rays, this is the line that is perpendicular with both the left ray and the right ray
- once this shortest line is found you can find the centre point of this line to estimate $\boldsymbol{P}$
![[Screenshot 2024-10-21 at 17.26.55.png|300]]
- find $a,b,c$ s.t: $a\boldsymbol{p}_L-bR^T\boldsymbol{p}_R-\boldsymbol{T}-c(\boldsymbol{p}_L\otimes R^T\boldsymbol{p}_R)=0$
	- given corresponding points, we know $\boldsymbol{p}_L, \boldsymbol{p}_R$
	- given calibrated views, we know $R, \boldsymbol{T}$
	- so $a\begin{bmatrix}\cdot\\\boldsymbol{p}_L\\\cdot\end{bmatrix}-b\begin{bmatrix}\cdot\\R^T\boldsymbol{p}_R\\\cdot\end{bmatrix}-c\begin{bmatrix}\cdot\\\boldsymbol{p}_L\otimes R^T\boldsymbol{p}_R\\\cdot\end{bmatrix}=\begin{bmatrix}\cdot\\\boldsymbol{T}\\\cdot\end{bmatrix}$
	- so $H\begin{bmatrix}a\\b\\c\end{bmatrix}=\boldsymbol{T}\Rightarrow \begin{bmatrix}a\\b\\c\end{bmatrix}=H^{-1}\boldsymbol{T}$
	![[Screenshot 2024-10-21 at 17.39.25.png|300]]
	- $\hat{\boldsymbol{P}}=(a\boldsymbol{p}_L+bR^T\boldsymbol{p}_R+\boldsymbol{T})/2$