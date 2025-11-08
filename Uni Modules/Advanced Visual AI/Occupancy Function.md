---
tags:
  - Implicit_Neural_Representations
---
#### Discrete
- $g(x,y,z)$ is binary
$$
g(x,y,z)=\begin{cases}1 & \text{if the point is inside the shape} \\ 0 & \text{if the point is outside the shape}\end{cases}
$$
- provides a basic, static way of determining if a point lies within or outside a 3D shape
#### Implicit
- *occupancy networks* are neural networks that learn to approximate the occupancy function of 3D shapes
- they provide a continuous representation of 3D geometry by predicting whether points in space are inside or outside a shape
- network outputs a probability:
	- $f_{\theta}(x,y,z)\rightarrow [0,1]$
	- where
		- $f_\theta$ is the learned function
		- $\theta$ are the network parameters
### Interpretation
- probability interpretation:
	- $f_\theta(x,y,z) > 0.5$: The point is likely inside the object
	- $f_\theta(x,y,z) < 0.5$: The point is likely outside the object
	- $f_\theta(x,y,z) = 0.5$: Indicates the point is on the object's surface boundary
- boundary interpretation
	- points with probabilities near $0.5$ are generally considered to be on or near the object's surface
	- this smooth transition allows the network to approximate complex shapes and intricate surface details