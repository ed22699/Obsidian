---
tags:
  - nerf_gaussian_splitting
---
- NeRF has several limitations
	- long training time
	- computational complexity (uses deep neural networks)
	- inefficiency in real-time use (heavy neural network calculations)
	- high memory consumption (dense neural networks demand significant memory resources)
	- difficult optimisation (involves complex optimisation processes which require fine-tuning multiple hyperparameters to achieve satisfactory results)
## Gaussian Splatting
- provides an alternative to [[NeRF]], using a different approach to represent the 3D scene
- represents the scene with a collection of oriented 3D Gaussians (instead of relying on a neural network)
- represents the scene by placing oriented 3D gaussians at various locations in space
	- each gaussian defined by its 
		- mean (position)
		- covariance (shape and orientation)
		- colour attributes
	- rendering achieved by projecting these gaussians onto the image plane and accumulating their contributions based on their projected densities and colours
- *Formula*: combines multiple gaussian functions to represent image intensity at each pixel location $(x,y)$
$$
I(x,y)=\sum_i w_i \cdot G(x,y|\mu_i, \Sigma_i)
$$
- where
	- $I(x,y)$: intensity value at position $(x,y)$ in the image
	- $G(x,y|\mu_i, \Sigma_i)$: gaussian function centred at $\mu _i$ with a covariance matrix $\Sigma_i$ which defines the spread and orientation of the gaussian
		- $\mu_i$: mean vector $(\mu_{x_i}, \mu_{y_i})$ specifying the centre location of the $i^{th}$ gaussian function in the image
		- $\Sigma_i$: the covariance matrix of the $i^{th}$ gaussian, controlling the gaussian's spread (size) and orientation (direction of spread)
	- $w_i$: a weight assigned to the $i^{th}$ gaussian, indicating its influence or contribution to the overall intensity $I(x,y)$ at point $(x,y)$
- gaussian function formula:
$$
G(x) = \exp(-\frac 1 2 (x-\mu)^T \Sigma^{-1}(x-\mu))
$$
- where
	- $x=(x,y)$: position vector
	- $\mu$: mean vector, indicating the gaussian centre
	- $\Sigma$: covariance matrix, influencing spread and orientation
- shape (spread)
	- eigenvalues of $\Sigma$ determine the spread along the principal axes
	- larger eigenvalues correspond to a broader spread
- orientation
	- eigenvectors of $\Sigma$ define the principal axes, setting the gaussian's direction in space
### Why fast
- compact representation
	- represents data points as gaussians, which are compact, making them efficient to compute
- efficient data aggregation
	- unlike discrete voxel-based or grid-based methods, gaussian splatting uses smooth, overlapping distributions, reducing the need for high-resolution grids
	- aggregation of overlapping gaussians can be done quickly with simple summation operations, avoiding the cost of complex interpolation
- parallelisation
	- gaussian operations can be efficiently parallelised on modern hardware such as GPUs, which significantly speed up computation
- sparse sampling
	- naturally fits well with sparse sampling methods, means fewer data points are needed compared to dense grids or meshes, leading to reduced computational load
- smooth function approximation
	- gaussian functions provide smooth and differentiable approximations of the underlying data, allowing rapid fitting and rendering without iterative refinement
![[Screenshot 2025-11-11 at 16.05.25.png|500]]
![[Screenshot 2025-11-11 at 16.05.53.png|500]]
### Applications
- real-time rendering
	- efficient computation, good for stuff such as VR and AR environments
- interactive scene exploration
	- allows users to interactively explore 3D scenes with smooth transitions and real-time updates
- mapping and reconstruction
	- can be used in 3D mapping and scene reconstruction with drones or autonomous vehicles, offering efficient processing of large-scale environments