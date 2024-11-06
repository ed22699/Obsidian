---
tags:
  - Lesson
  - motion_estimation
---
# Motion Estimation
- estimation of the 2D motion field from frames in an image sequence
- using spatial and temporal variation of pixel values
	- relationship between variation in pixel values (known as apparent motion or optical flow) and the true motion is not straightforward
## Apparent versus True Motion
- apparent motion or optical flow is the perceived motion in video sequence caused by changes in pixel values
- relationship with true 2D motion field is not always straightforward
	- extreme cases can complicate this:
		- non-zero apparent motion for zero motion field e.g. static scene, moving light source
		- zero apparent motion for non-zero motion field, e.g. constant colour sphere rotation in diffuse lighting
- sometimes it is not possible to determine 2D motion field without additional constraints or assumptions
	- we assume optical flow results from brightness constancy constraint
		- a moving pixel retains its value between frames
		- this is natural to assume, if we are taking enough frames per second this is a valid assumption as there will only be small changes. With larger gaps between frames, factors such as illumination can effect this
	- for continuous video $I(x,y,t)$ (grey level)
		- $I(x+\Delta x, y+\Delta y, t+\Delta t) = I(x,y,t)$ 
		- using Taylor's expansion: $I(x+\Delta x, y+\Delta y, t+\Delta t) = I(x,y,t)+\frac{\delta I}{\delta x}\Delta x+\frac{\delta I}{\delta y}\Delta y+\frac {\delta I}{\delta t}\Delta t+...$
## Optical Flow Equation (OFE)
![[Screenshot 2024-11-04 at 22.40.50.png|150]]
- for $I(x+\Delta x, y+\Delta y, t+\Delta t) = I(x,y,t)$ 
	- $\frac{\delta I}{\delta x}\Delta x+\frac{\delta I}{\delta y}\Delta y+\frac {\delta I}{\delta t}\Delta t=0$
	- dividing throughout by $\Delta t$: $\frac{\delta I}{\delta x}\frac{\Delta x}{\Delta t}+\frac{\delta I}{\delta y}\frac{\Delta y}{\Delta t}+\frac {\delta I}{\delta t}=0$
	- for $\Delta x, \Delta y, \Delta t \rightarrow 0$: $\frac{\delta I}{\delta x}\frac{dx}{dt}+\frac{\delta I}{\delta y}\frac{dy}{dt}+\frac {\delta I}{\delta t}=0$ (OFE)
		- $\frac{dx}{dt}, \frac{dy}{dt}$: rate of change of $x,Y$ with time $\rightarrow$ optical flow field $\boldsymbol u = (u_x, u_y)$
		- $\frac{\delta I}{\delta x}, \frac{\delta I}{\delta y}, \frac{\delta I}{\delta t}$: rate of change of $I$ with $x,y,t \rightarrow$ spatial and temporal gradients $(I_x,I_y,I_t)$
	- optical flow equation: $I_xu_x+I_yu_y+I_t=0$
		- for $\boldsymbol u=(u_x,u_y)$ and $\nabla I=(I_x,I_y)$: $I_xu_x+I_yu_y+I_t=0\rightarrow \nabla I\cdot u+I_t=0$
			- $\nabla I\cdot u=I_xu_x+I_yu_y$ 
- OFE alone is not sufficient to estimate motion as only one equation in two unknowns. It can only estimate **normal flow** $u_n$ 
	- $\nabla I\cdot u+I_t=\nabla I\cdot u_n+I_t=0 \Rightarrow ||u_n||=-I_t/||\nabla I|| \quad \angle u_n = \angle \nabla I$ 
		- $u=u_p+u_n$
		- $u_p\cdot u_n = 0$
		- $\nabla I\cdot u_p=0$
## Normal Flow
- $\nabla I\cdot u+I_t=\nabla I\cdot u_n+I_t=0 \Rightarrow ||u_n||=-I_t/||\nabla I|| \quad \angle u_n = \angle \nabla I$ 
![[Screenshot 2024-11-04 at 22.40.11.png|100]]
- **Aperture Problem**: with single gradient direction in window (aperture), observed motion is different from true motion as we can only observe motion parallel to the gradient
	- hence: Good motion estimation depends on having sufficient variation in spatial gradient within regions
		![[Screenshot 2024-11-04 at 22.39.36.png|200]]
	- note the red apertures cannot predict the true motion
	- need aperture on the edges to view any motion
- why don't I make my regions of apertures very big?
	- potentially different motion in every pixel so a big aperture will likely see lots of motions, this won't really help us. Lots of spatial gradients but lots of motions
- why don't I make my regions of apertures very small?
	- more likely to get just a single spatial gradient
## Constraining the OFE
- OFE is under constrained - can only estimate normal flow, we need to add extra constraints, e.g. assume parametric form of motion field in regions
	- assume each of these four motion vectors are the same (not unreasonable unless when we are looking at an edge as there is a large change in depth it will create a large motion vector)
	- assume constant velocity is linear in $x$ and $y$
		- $u_x=ax+by+c$
		- $u_y=dx+ey+f$
### Constant Velocity Model
- for a region, find the velocity $\boldsymbol u=(u_x,u_y)$ which minimises: $\mathcal E(u_x,u_y)=\sum_{region}(I_xu_x+I_yu_y+I_t)^2$ (same $\boldsymbol u$ over whole region)
	- rather than wanting $0$ over a pixel we are looking to get $0$ over a whole region
### Lucas and Kanade Algorithm
- finds the velocity $\boldsymbol u=(u_x,u_y)$ which minimises $\mathcal E(u_x,u_y)$
- gets the partial derivatives of $\mathcal E(u_x,u_y)$ w.r.t $u_x$ and $u_y$, sets them to zero and solves for $u_x$ and $u_y$
	- $\frac {d \mathcal E}{d u_x}=2\sum_R(I_xu_x+I_yu_y+I_t)I_x=0 \Rightarrow \sum_R(I^2_xu_x+I_xI_yu_y+I_xI_t)=0$
	- $\frac {d \mathcal E}{d u_y}=2\sum_R(I_xu_x+I_yu_y+I_t)I_y=0 \Rightarrow \sum_R(I_xI_yu_x+I^2_yu_y+I_yI_t)=0$
- hence given that:
	- $u_x\sum_RI_x^2+u_y\sum_RI_xI_y=-\sum_RI_tI_x$
	- $u_x\sum_RI_xI_y+u_y\sum_RI_y^2=-\sum_RI_tI_y$
	- $\Rightarrow Au = b$
		- $u=\begin{bmatrix}u_x\\u_y\end{bmatrix}=A^{-1}b$
		- $A=\sum_R\begin{bmatrix}I_x^2 & I_xI_y\\I_xI_y & I_y^2\end{bmatrix}$ (this is a convolution matrix)
		- $b=-\sum_R\begin{bmatrix}-I_tI_x\\-I_tI_y\end{bmatrix}$
![[Screenshot 2024-11-06 at 10.28.06.png|400]]
![[Screenshot 2024-11-06 at 10.28.30.png|100]]
- this algorithm can go wrong when $A$ does not have an inverse
	- the scenario for this will typically be when our region is over an edge or when all the spatial gradients are $0$
	- should have a check to see if there is an inverse, no inverse when the determinant of $A$ is $0$
### Spatial and Temporal Gradients
where does $I_x, I_y$ and $I_t$ come from?
- Approximate gradients using differences, e.g. $I_x=\frac {\delta I}{\delta x}\approx I(x+1,y,t)-I(x,y,t)$
	- i.e. assume $\delta x=1$
	- is the rate of change of $I$ with $x$
	- basically assuming a straight line in the spatial gradient
	![[Screenshot 2024-11-06 at 10.24.54.png|150]]
- or use averaging to reduce noise, e.g. $I_x \approx (I_x^a+ I_x^b+I_x^c+ I_x^d)/4$
	![[Screenshot 2024-11-06 at 10.27.13.png|120]]
>[!note]
below is not on the test
# Multiresolution L&K
- to deal with large motions, implement L&K over multiple resolutions - result at lower resolutions used to 'warp' higher resolution images prior to estimation (like with [[Scale-Invariant Feature Transform (SIFT) Matching]])
![[Screenshot 2024-11-06 at 10.34.29.png|200]]
# Affine Motion Model
- $u=Ap$ coming from:
	- $u_x=ax+by+c$
	- $u_y=dx+ey+f$
	- $p^T=(a,b,c,d,e,f)$
- models translation, scaling, rotation and shear
- $p^TA^T\nabla I+I_t=0$ affine OFE $\Rightarrow \hat p + M^{-1}\boldsymbol b$
	- $M=\sum_{region}A^T\nabla I\nabla I^TA$
	- $b=-\sum_{region}I_t(A^T\nabla I)$
