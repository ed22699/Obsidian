---
tags:
  - nerf_gaussian_splitting
---

![[Screenshot 2025-11-09 at 15.43.21.png|400]]
- *Input*: A set of camera poses $\{x_c, y_c, z_c, \gamma_c, \theta_c\}_n$ 
	- $n$: number of different camera poses used to capture different perspectives of the scene
	- $x_c, y_c, z_c$: Coordinates representing the camera's position in the 3D space
	- $\gamma_c, \theta_c$: Angles (the inclination and azimuth angles) representing the orientation of the camera
- *Output*: A bundle of rays for each pose $\{o,d\}_{H\times W\times n}$
	- $H$: height of the image plane, representing the vertical resolution
	- $W$: width of the image plane, representing the horizontal resolution
	- $n$: number of camera poses, matching the input set
	- $o$: the origin of each ray, which starts from the camera
	- $d$: the direction vector for each ray, pointing into the 3D scene
![[Screenshot 2025-11-09 at 15.48.12.png|200]]
- Parametric equation to define any point on the ray: 
$$
r(t) = o + td
$$
- where
	- $o$ is the origin of the rays
	- $d$ is the direction vector
- ray marching is the process of *casting rays from the camera into the scene* and *sampling points along these rays* to *determine the visual properties* (e.g. colour and density) at each point
- Backward tracing is used
	- follows the path of light from the camera to the object 
	- called backward tracing because it *traces rays starting from the camera (observer)* and marching toward the object
		- in contrast to traditional ray tracing what often starts from light sources