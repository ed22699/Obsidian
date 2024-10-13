---
tags:
  - stereo_and_motion
---
- geometry depends on position and orientation of cameras
- epipolar geometry
- reminder [[rotation matrices]]
![[Screenshot 2024-10-13 at 18.27.28.png|400]]
- 3D coordinate transformations:
	- $\boldsymbol{P}_W$ - vector defining $P$ in world coordinates
	- $\boldsymbol{P}_C$ - vector defining $P$ in camera coordinates
	- $\boldsymbol{T}$ - 3D camera position vector
	- $R$ - 3D camera rotation matrix
		- define rotation to be applied to camera coordinate system to align it with world coordinate system
	![[Screenshot 2024-10-13 at 18.31.25.png|200]]
	- $\boldsymbol{P}_C=R(\boldsymbol{P}_W-\boldsymbol{T})$
	- $\boldsymbol{P}_W=R^{-1}\boldsymbol{P}_C+\boldsymbol{T}=R^T\boldsymbol{P}_C+\boldsymbol{T}$
		- rotation matrix $R^T=R^{-1}$ 
- Homogeneous Coordinates
	- allow coordinate transformations to be defined by 4x4 matrices
	- $I$ - identity matrix
	- $\boldsymbol{P}'_W=\begin{bmatrix}X_W\\Y_W\\Z_W\\1\end{bmatrix}=\begin{bmatrix}\boldsymbol{P}_W \\ 1\end{bmatrix}$
		- $\begin{bmatrix}\boldsymbol{P}_W\\1\end{bmatrix}=\begin{bmatrix}R^T & \boldsymbol{T}\\0 & 1\end{bmatrix}\begin{bmatrix}\boldsymbol{P}_C \\1\end{bmatrix}=H_{CW}\boldsymbol{P}'_c \Rightarrow \boldsymbol{P}_W=R^T\boldsymbol{P}_C+\boldsymbol{T}$    
		- $H_{CW}$ - camera to world coordinate transformation matrix
			- $H_{CW}=\begin{bmatrix}R_{00}&R_{10}&R_{20}&T_x\\R_{01}&R_{11}&R_{21}&T_{y}\\R_{02}&R_{12}&R_{22}&T_z\\0&0&0&1\end{bmatrix}$ 
	- $\boldsymbol{P}'_C=H_{CW}^{-1}\boldsymbol{P}'_W=H_{WC}\boldsymbol{P}'_W\Rightarrow \boldsymbol{P}_C=R(\boldsymbol{P}_W-\boldsymbol{T})$
		- $H_{WC}=\begin{bmatrix}R&-R\boldsymbol{T}\\0&1\end{bmatrix}\Rightarrow H_{WC}H_{CW}=I$ 
- Stereo Coordinate Systems
	- $\boldsymbol{P}'_L=H_{WL}\boldsymbol{P}'_W=H_{WL}H^{-1}_{WR}\boldsymbol{P}'_R=H_{RL}\boldsymbol{P}'_R$
		- $H_{RL}=\begin{bmatrix}R^T & \boldsymbol{T}\\0&1\end{bmatrix}$ 
	- $\boldsymbol{P}_L=R^T\boldsymbol{P}_R+\boldsymbol{T}$
	- $\boldsymbol{P}'_R=H_{WR}\boldsymbol{P}'_W$
	- $\boldsymbol{P}_R=R(\boldsymbol{P}_L-\boldsymbol{T})$
![[Screenshot 2024-10-13 at 19.02.43.png|300]]
	