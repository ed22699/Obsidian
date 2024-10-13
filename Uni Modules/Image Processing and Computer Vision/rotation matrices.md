---
tags:
  - stereo_and_motion
---
- 2D counter-clockwise rotation for a 2x2 matrix matrix:
$$
\boldsymbol{v}'=\begin{bmatrix}v'_x\\v'_y\end{bmatrix}=\begin{bmatrix}\cos \theta & -\sin\theta \\ \sin\theta & \cos\theta\end{bmatrix}\begin{bmatrix}v_x \\ v_y\end{bmatrix}=R(\theta)\boldsymbol{v}
$$
- 3D rotation composed of rotations around $X$, $Y$ and $Z$ axis: $R=R_XR_YR_Z$
- clockwise rotation about $Y$ axis:
$$
R_Y\boldsymbol{P}=\begin{bmatrix}\cos\theta_Y & 0 & \sin\theta_Y \\ 0 & 1 & 0 \\ -\sin\theta_Y & 0 & \cos\theta_Y\end{bmatrix}\begin{bmatrix}X\\Y\\Z\end{bmatrix}
$$
