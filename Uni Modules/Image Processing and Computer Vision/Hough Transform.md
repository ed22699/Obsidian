---
tags:
  - edge_shape
---
- image space transformed into a parameter space
- voting procedure is carried out in the parameter space and object candidates are obtained as local maxima
### Line Representation
- Hough transform uses the parametric equation to plot lines as many will not cross the origin
- $f(x,y,\rho,\theta)=x\cos \theta +y\sin\theta-\rho=0$
	- $\rho$ is the distance between the straight line and the origin
	- $\theta$ is the angle between the distance vector and the positive $x$-direction
	![[Screenshot 2024-09-30 at 08.42.51.png|300]]
## Method
- at each 'edge' plot lines in all directions and add them to the hough space
	- a point $(x,y)$ in the image space is transformed into a sinusoidal curve in the parameter space
	- point $(\rho, \theta)$ on this sinusoidal cure represents a straight line passing through the point $(x,y)$ in the image space
![[Screenshot 2024-09-30 at 08.47.11.png|300]]
- as more lines are drawn more points become popular in the hough space, i.e. the probability that a line is an edge becomes more likely
![[Screenshot 2024-09-30 at 08.49.06.png|400]]
### Algorithm
1. Make available an $n=2$ dimensional array $H(\rho,\theta)$ for the parameter space
2. find the gradient image: $G(x,y)=|G(x,y)|\angle G(x,y)$
3. for any pixel satisfying $|G(x,y)|>T_{s}$, increment all elements on the curve $\rho = x\cos \theta + y\sin \theta$ in the parameter space represented by the $H$ array:
$$
\forall \theta |\rho=x\cos \theta+y\sin \theta
$$
$$
H(\rho, \theta)=H(\rho,\theta)+1
$$
4. in the parameter space, any element $H(\rho, \theta) > T_{h}$ represents a straight line detected n the image