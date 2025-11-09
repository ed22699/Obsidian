---
tags:
  - nerf_gaussian_splitting
---
![[Screenshot 2025-11-09 at 15.41.05.png|400]]
- Neural Radiance Fields aims to render high-quality images based on the pose of the camera
- model learns a *continuous volumetric scene function* that assigns a colour and volume density to any voxel in space
### Step 1: Ray Marching
![[Ray Marching]]
### Step 2: Collecting Query Points
- *Input*: bundle of rays for every pose $\{o,d\}_{H\times W\times n}$
- *Output*: set of 3D query points $\{x_p, y_p, z_p\}_{n\times m\times H \times W}$
	- $m$ represents the number of points sampled along each ray
- rays pass through 3D space, collecting points of interest
- Query points $\{x_p, y_p, z_p\}$ are collected along the ray
- uniform sampling along rays with $m$ points per ray
$$
p_i = o +t_i \cdot d \; for \; i=1,...,m
$$
- where
	- $p_i$ represents the specific 3D coordinates of a point along a ray at step $i$
	- query points $\{x_p, y_p, z_p\}$ represent the coordinates of the samples points in 3D space, which are essentially the $p_i$ values for different rays and steps
![[Screenshot 2025-11-09 at 16.00.09.png|400]]
**Volume rendering side note??**
### Volume Rendering
- *Input*: A set of 3D query points + their volume profile (volume density) $\sigma +$RGB value
$$
\{x_p, y_p, z_p, RGB, \sigma \}_{n\times m\times H\times W}
$$
- *Output*: a set of rendered images (one per pose)
$$
\{H,W\}_n
$$
- use the rendering equation (continuous form) to determine the final colour $C(r)$ of the pixel (on the rendered image) observed along a ray $r(t)=o+td$ 
$$
C(r)= \int_{t_n}^{t_f} T(t)\sigma (r(t))c(r(t), d)dt
$$
