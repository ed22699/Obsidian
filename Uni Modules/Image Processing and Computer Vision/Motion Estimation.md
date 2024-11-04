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
- **Ap








assume optical flow results from brightness constancy constraint
- natural to assume, if we are taking enough frames per second this is a valid assumption as there will only be small changes. With larger gaps between frames, illumination can effect this

you can only predict the motion perpendicular to the edge (you can only be sure of $u_n$ in normal flow) $\rightarrow$ aperture problem
- aperture is a region within our frame where we are viewing this motion
- why don't I make very big aperture?
	- motion in a scene typically has motion going in different directions, this will be lost with a big aperture
- why don't I make a very small aperture
	- motion with potentially each pixel, within the entire image due to depth, etc, leads to a lot of motion which you can't do much with
predicting motion is bad when it comes to edge as will suddenly have a large depth between two points so will be viewed as a large change

$A$ will not have an inverse when our region is over an edge
- will not have an inverse is determinant of $A$ is $0$ 
issue when motion within the region is all in different directions