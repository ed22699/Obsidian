---
tags:
  - Lesson
  - motion
---
# Video Sequences
![[Screenshot 2024-11-03 at 11.50.21.png|200]]
# Modelling 2D Motion Fields
- either the camera moves or the object moves, becomes tricky when they both move
![[Screenshot 2024-11-03 at 11.52.39.png|400]]
- equations for both movements are exactly the same
## Incremental 2D Motion Fields
find relationship between the:
- position of a 3D point and its 2D motion
- 2D motion of different 3D points
- 3D motion of a 3D point and its 2D motion
## 3D Rigid Motion
![[Screenshot 2024-11-03 at 11.56.13.png|200]]
- $P'=RP+T$
	- $R$: 3x3 rotation matrix
	- $T$: 3x1 translation vector
- in rigid motion objects do not deform
### Rotation Matrices
- $R=R_XR_YR_Z$: rotations about $X$, $Y$, and $Z$ axes
	- $R_YP=$$\begin{bmatrix}\cos\theta_Y &0&\sin\theta_Y\\0&1&0\\-\sin\theta_Y&0&\cos\theta_Y\end{bmatrix}\begin{bmatrix}X\\Y\\Z\end{bmatrix}=\begin{bmatrix}X\cos\theta_Y+Z\sin\theta_Y\\Y\\Z\cos\theta_Y-X\sin\theta_Y\end{bmatrix}$
		-  for small $\theta_Y$: $R_Y\approx\begin{bmatrix}1&0&\theta_Y\\0&1&0\\-\theta_Y&0&1\end{bmatrix}$
		- for small $\theta_Y$: 
			- $\cos\theta_Y\approx 1$
			- $\sin\theta_Y\approx\theta_Y$
	- for small $\theta_X,\theta_Y,\theta_Z$: $R\approx\begin{bmatrix}1&-\theta_Z&\theta_Y\\\theta_Z&1&-\theta_X\\-\theta_Y&\theta_X&1\end{bmatrix}$
- with motion we use frames close together compared to stereo where we will use key frames, further apart
	- we can use small angle approximation as we are assuming there is a small change in angle per frames as we are looking at close together frames
## 3D Motion Field
![[Screenshot 2024-11-03 at 12.18.00.png|100]]
- $V=\lim_{\Delta t\rightarrow 0}\{P'-P=(R-I)P+T\}$
	- call back to $P'=RP+T$
	- so using the small angle approx for $R$ we get:
		- $V_X=\theta_YZ-\theta_ZY+T_X$
		- $V_Y=\theta_ZX-\theta_XZ+T_Y$
		- $V_Z=\theta_XY-\theta_YX+T_Z$
- $(\theta_X,\theta_Y,\theta_Z)\equiv$ angular velocity
- $(T_X,T_Y,T_Z)\equiv$ rectilinear velocity
>[!note]
if you rotate a camera but it remains in the same place motion field is independent of depth

## 2D Motion Field Equations
- for image point $p=(x,y,f)$ with motion field $v=(v_x,v_y)$
	- $v_x=\frac{dx}{dt=\frac d{dt}(\frac{fX}Z)=f\frac{V_XZ-XV_Z}{Z^2}}$
	- 