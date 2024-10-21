---
tags:
  - Lesson
  - epipolar_geometry
---
[[Stereo Geometry]]
- Epipolar geometry defines relationship between two stereo views
- for unknown viewpoints, given matching points it enables estimation of viewpoints
- for known viewpoints, it constrains matches to lie along epipolar lines
## Epipolar Lines
![[Screenshot 2024-10-21 at 12.12.24.png|300]]
1. extend a ray into 3D from $\boldsymbol{p}_L$ and pick a point along that ray and project it into the right camera
2. repeat with other points
	- this forms a line in the right camera - epipolar line
		- forms a plane in 3D where all lines should lie, as this is a plane cutting a plane, they all lie on a line
	- don't know depth, do know the corresponding point that lies across the line
	- every point in the left camera has a corresponding line in the right camera
		- taking other points in the left will form lines in the right of different orientation (will be similar)
3. if you do the same with the right camera, you end up with an epipolar line that lies in the same plane. For these two points we end up with the epipolar plane
- where the line between the two centres of projection, where they cut the image plane is known as the epipole
	- all epipolar lines all end up at the epipoles
##  Epipolar Line Constraint
![[Screenshot 2024-10-21 at 12.26.11.png|200]]
- rigid transformation between cameras: $\boldsymbol{P}_R=R(\boldsymbol{P}_L-\boldsymbol{T})$
- perspective projection:
	- $\boldsymbol{P}_L=\begin{bmatrix}X_L\\Y_L\\Z_L\end{bmatrix}$
	- $\boldsymbol{p}_L=\begin{bmatrix}x_L\\y_L\\f\end{bmatrix}=\frac{f\boldsymbol{P}_L}{Z_L}$
	- $\boldsymbol{p}_R=\begin{bmatrix}x_R\\y_R\\f\end{bmatrix}=\frac{f\boldsymbol{P}_R}{Z_R}$
- vectors $\boldsymbol{P}_L$, $\boldsymbol{T}$ and $\boldsymbol{P}_L-\boldsymbol{T}$ all lie in a plane
	- $(\boldsymbol{T}\otimes\boldsymbol{P}_L)$ - perpendicular to plane
		![[Screenshot 2024-10-21 at 12.26.37.png|100]]
		- $(\boldsymbol{T}\otimes\boldsymbol{P}_L)=S\boldsymbol{P}_L$  
			- $S=\begin{bmatrix}0 &-T_Z&T_Y\\T_Z&0&-T_X\\-T_Y&T_X&0\end{bmatrix}$
	- $(\boldsymbol{P}_L-\boldsymbol{T})^T(\boldsymbol{T}\otimes\boldsymbol{P}_L)=0$ (dot product for perpendicular vectors)
		- $\boldsymbol{P}_R=R(\boldsymbol{P}_L-\boldsymbol{T})$
		- $R^T\boldsymbol{P}_R=(\boldsymbol{P}_L-\boldsymbol{T})$
			- $R^T=R^{-1}$
		- $\boldsymbol{P}_R^TR=(\boldsymbol{P}_L-\boldsymbol{T})^T$
	- $\boldsymbol{P}_R^TRS\boldsymbol{P}_L=0$ 
		- if you take a vector defining a point in the left coordinate system and a vector defining the same point in the right coordinate system, they are defined through this relationship
![[Screenshot 2024-10-21 at 12.39.58.png|300]]
- $\boldsymbol{P}_R^TRS\boldsymbol{P}_L=0 \Rightarrow \boldsymbol{P}_R^TE\boldsymbol{P}_L=0$
	- $E=RS$ is the essential matrix
		- 3x3 matrix
		- all the epipolar lines are defined by this matrix
- $\boldsymbol{P}_R^TE\boldsymbol{P}_L=0 \Rightarrow \frac{Z_R}f\boldsymbol{p}_R^TE\frac{Z_L}f\boldsymbol{p}_L=0\Rightarrow \boldsymbol{p}_R^TE\boldsymbol{p}_L=0$ 
	- $\boldsymbol{p}_L=\frac{f\boldsymbol{P}_L}{Z_L}\Rightarrow \boldsymbol{P}_L=\frac{Z_L\boldsymbol{p}_L}{f}$
	- $\boldsymbol{p}_R=\frac{f\boldsymbol{P}_R}{Z_R}\Rightarrow \boldsymbol{P}_R=\frac{Z_R\boldsymbol{p}_R}{f}$
	- original relationship in terms of 3D points is the same for 2D points as $\boldsymbol{p}_R$ are scaler versions of $\boldsymbol{P}_R$ so constraint itself doesn't change
	
