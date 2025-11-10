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
	- continuous form integrates the colour contribution along a ray over a continuous path through the volume
	- integral accumulates the colour contributions from each point along the ray, weighted by the transmittance and density, to produce the final colour observed
$$
C(r)= \int_{t_n}^{t_f} T(t)\sigma (r(t))c(r(t), d)dt
$$
- where
	- $C(r)$: final colour observed along the ray $r$
	- $r(t)$: position along the ray $r$ at depth $t$
		- represents the 3D coordinates through which the ray travels within the scene
	- $t_n$ and $t_f$: near and far bounds of integration along the ray
		- define the starting and ending points (in depth) of the ray as it passes through the volume
	- $T(t) = \exp (-\int_{t_n}^t \sigma(r(s))ds)$:
		- transmittance: $T(t)$ represents the fraction of light that reaches depth $t$ without being absorbed
		- $\int _{t_n}^t \sigma (r(s)) ds$ computes the cumulative volume density (or opacity) from the starting point $t_n$ to the current depth $t$
		- exponential decay: transmittance decreases exponentially with distance
			- as it accumulates the effect of density over distance
			- higher density along the path increases absorption and decreases $T(t)$
	- $\sigma(r(t))$: volume density at position $r(t)$
		- representing how much light is absorbed per unit distance at that point
		- higher $\sigma$ imply more absorption (opacity)
		- lower $\sigma$ imply transparency
	- $c(r(t), d)$: colour (or radiance) at point $r(t)$ in the direction $d$
		- describes the colour contribution of the point along the ray, taking into account the light emitted or reflected at that location
	- $dt$: the infinitesimal thickness of each slice along the ray, indicating that this is a continuous integration
#### Rendering Equation (Discrete)
- continuous integral is approximated by a sum over $N$ discrete sample points along the ray
$$
C(r) \approx \sum_{i=1}^N T_i \alpha _i c_i
$$
- where
	- $\alpha _i = 1 - \exp(-\sigma _i \delta _i)$ represents the probability of light being scattered at $t_i$
	- $\delta _i = t_{i+1}-t_i$ is the distance between adjacent samples
	- $\sigma _i = \sigma (r(t_i))$ and $c_i = c(r(t_i), d)$
	- $T_i = \prod _{j=1} ^{i-1}(1-\alpha_j)$ is the accumulated transmittance up to $t_i$
### Neural Network Inference
- *Input*: Encoded query points
- *Output*: RGB colour and volume density for each point
- network learns to represent the colour and density profiles along each ray
- the neural network is used to predict the colour and density at each query point based on the encoded representation
- Neural networks struggle to perform inference directly on the raw 3D coordinates $\{x_p, y_p, z_p\}$ 
	- challenge lies in the nature of them being high-frequency signals, especially with detailed geometry or rapid variations in 3D space
	- standard neural networks have a learning bias towards low-frequency functions
		- *struggle to accurately approximate functions that vary rapidly*
		- known as the *spectral bias* of neural networks
			- tend to prioritise learning smooth low-frequency components first
	- without proper transformation, the network finds it difficult to represent fine details of the scene, leading to over-smoothed or blurred renderings
### Step 3: Positional Encoding
- *Input*: A set of 3D query points $\{x_p, y_p, z_p\}_{n\times m \times H \times W}$
- *Output*: A set of query points embedded into d-dimensional space $\{x_1, x_2, ..., x_d\}_{n \times m \times H \times W}$ 
- encoded representation allows the network to effectively capture high-frequency variations in the 3D space
- encoding function:
$$
\gamma (p) = (\sin(\pi p), \cos(\pi p), \sin(2\pi p), \cos(2\pi p),...)
$$
- high-frequency features help the network better represent detailed geometry and colours
- positional encoding helps to overcome the limitations of neural networks in representing high-frequency details effectively
### Step 4: Neural Network Inference
- *Input*: A set of 3D query points (after positional encoding)
	- $\{x_1, x_2, ..., x_d\}_{n\times m \times H\times W}$
	- each $x_i$ is a positional encoding of the 3D query points across dimensions $n\times m\times H\times W$
- *Output*: RGB colour and volume density for each query point
	- $\{RGB, \sigma\}_{n\times m \times H \times W}$
	- where
		- $RGB$ represents the colour values $(R,G,B)$ in the range $[0,1]$
		- $\sigma$ is the volume density (opacity) at each point
- neural network (MLP) learns to represent the colour and density profiles along each ray by predicting both the colour RGB and density $\sigma$ at each query point based on its encoded representation
### Step 5: Volume Rendering
- *Input*: set of 3D query points (after positional encoding) with their volume profile and RGB colour values
	- $\{x_1, x_2, ..., x_d, RGB, \sigma\}_{n\times m \times H\times W}$
	- where
		- query points $\{x_1, x_2, ...,x_d\}$ has an associated RGB colour and volume density $\sigma$
		- dimensions $n \times m \times H\times W$ represent multiple instances, features, and image resolution
- *Output*: set of rendered images (one per pose)
	- $\{H, W\}_n$
	- where
		- $h$ and $W$ are the height and width of each image
		- $n$ is the number of poses
### Neural Network Training
- Train with labels and ground truth:
	- set of rendered images (one per pose): $\{H, W\}_n$
	- set of ground truth images (one per pose): $\{H,W\}_{n,gt}$
- loss function
	- L2 loss between the rendered images and ground truth images calculated as a single scalar value: $\{l\}_n$
	- compute the L2 loss between each rendered image and corresponding ground truth image
	$$
	L=\sum_{i=1}^n ||I_{rendered}^{(i)}-I_{gt}^{(i)}||^2
	$$
	- the computed loss $L$ is then backpropagated to optimise the neural network weights, helping to im