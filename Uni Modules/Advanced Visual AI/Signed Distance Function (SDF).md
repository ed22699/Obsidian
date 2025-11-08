---
tags:
  - Implicit_Neural_Representations
---
### Signed Distance Function
#### Discrete
- signed distance values:
	$$
	g(x,y,z)= \begin{cases}-d & \text{if the point is inside the shape} \\ +d & \text{if the point is outside the shape}\end{cases}
	$$
- boundary condition: 
	- if $d=0$ the point lies exactly on the surface, allowing precise boundary definition
#### Implicit
- DeepSDF (Signed distance function) is a neural network based method for representing 3D shapes as a continuous signed distance field (SDF)
$$f_\theta (x,y,z) = d$$
- where
	- $\theta$ represents the parameters learned by the neural network
	- $d$ is the signed distance
		- $d < 0$: inside the object
			- the more negative $d$ is, the deeper the point is within the object
		- $d>0$: outside the object
			- larger values of $d$ indicate a greater distance from the surface
		- $d=0$: on the surface of the object
			- the zero-crossing defines the precise boundary shape