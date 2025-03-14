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
## 2D Motion Field Equations
- for image point $p=(x,y,f)$ with motion field $v=(v_x,v_y)$
	- $v_x=\frac{dx}{dt}=\frac d{dt}(\frac{fX}Z)=f\frac{V_XZ-XV_Z}{Z^2}$
		- $x=\frac{fX}Z$
		- $V_X=\frac{dX}{dt}$
		- uses quotient rule: $\frac{dy}{dx}=\frac{v\frac{du}{dx}-u\frac{dv}{dx}}{v^2}$
- if you substitute for $V_X,V_Y,V_Z$ you get
	- $v_x=\frac{(fT_X-xT_Z)}Z+f\theta_Y-\theta_Zy-\frac{(\theta_Xxy-\theta_Yx^2)}f$
	- $v_y=\frac{(fT_y-yT_Z)}Z - f\theta_X+\theta_Zx+\frac{(\theta_Yxy-\theta_Xy^2)}f$
- in the equations for $v_x$ and $v_y$ there are two components:
	- translational component - dependent on the scene depth $Z$ only affects the first section
	- rotational component - independent of scene depth $Z$ (second section)
![[Screenshot 2024-11-03 at 12.37.03.png|400]]
>[!note]
if you rotate a camera but it remains in the same place motion field is independent of depth

![[Screenshot 2024-11-03 at 12.40.27.png|300]]
### Special Case: Pure Translation
- assume 3D motion is only translational $\theta=0$
	- $v_x=\frac{(fT_X-xT_Z)}Z$
	- $v_y=\frac{(fT_Y-xT_Z)}Z$
- if $T_Z\neq 0,x_0=fT_X/T_Z$ and $y_0=fT_Y/T_Z$, then
	- $v_x=\frac{-(x-x_0)T_Z}Z$
	- $v_y=\frac{-(y-y_0)T_Z}Z$
- expansion - object moving towards camera ($T_Z$ negative)
![[Screenshot 2024-11-03 at 12.46.28.png|150]]
- contraction - object moving away from camera ($T_Z$ positive)
![[Screenshot 2024-11-03 at 12.47.27.png|150]]
- $(x_0,x_0)$ - focus of expansion (contraction)
### Special Case: Moving Plane
- assume 3D points lie in plane with unit surface normal $N$, i.e. $N^TP=d$, where $d$ is distance of plane from origin
![[Screenshot 2024-11-03 at 12.52.07.png|100]]
- since $P=Zp/f$, this gives $Z(N_Xx+N_Yy+N_Zf)/f=d$
- substituting for $Z$ in 2D motion field:
	- $v_x=\frac 1 {fd}(a_1x^2+a_2xy+a_3fx+a_4fy+a_5f^2)$
	- $v_y=\frac{1}{fd}(a_1xy+a_2y^2+a_6fy+a_7fx+a_8f^2)$
- motion field is a quadratic polynomial in 2D spatial coordinates $x$ and $y$
>[!note]
small portions of a scene are often planes