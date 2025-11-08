---
tags:
  - Implicit_Neural_Representations
---
## 2D Images
- in practice, $f$ can be parameterised by a neural network to enable continuous, resolution-independent sampling
	$$
	f_\theta (x,y)=\sigma (W_n ... \sigma(W_1[x,y]+b_1)+b_n)
	$$
- where:
	- $\theta = \{W_i, b_i\}$: learnable parameters of the neural network
		- $W_i$: represents the weights in layer $i$ of the neural network
		- $b_i$: represents the biases in layer $i$ of the neural network
	- $\sigma$: non-linear activation function used to capture high-frequency details
- $f_\theta$ can be trained to output RGB values for any given resolution making it adaptable to different sampling spaces
- *Aim*: 
	- train the neural network $f_\theta (x,y,h,w)$ to approximate a continuous function by learning a mapping from spatial coordinates $(x,y)$ to target values
	- specifically, train on an image of size $N\times M$ pixels, where $N$ is the hight and $M$ is the width
- *training data* used:
	- use pairs of pixel coordinates $(x_i, y_i)$ and their corresponding RGB values target:
	$$
	\{(x,y)\rightarrow RGB(x,y)\} \; for \; x=1,...,N \;and \; y=1,...,M
	$$
	- each pixel in the $N\times M$ image provides a training sample, allowing the model to learn a continuous approximation of the image
- *Loss function*:
	- MSE loss function for training the INR model on an image of size $N\times M$ pixels is:
	$$
	L(\theta) = \frac 1 {NM} \sum_{x=1}^N \sum_{y=1}^M || I(x,y)-f_\theta (x,y)||^2
	$$
	- where:
		- $I(x,y)$ is the true RGB value at pixel $(x,y)$ 
		- $f_\theta(x,y)$ is the predicted RGB value from the neural network
- *Optimisation*:
	- update $\theta = \{W_i, b_i \}$ using gradient descent (e.g. [[Adam]] optimiser) to minimise $\mathcal L(\theta)$ 
	- continue training until the network accurately represents the image
-  *Result*:
	- once trained, the model can generate RGB values at any coordinate, enabling high-resolution sampling of the image, even beyond $N\times M$ pixels
### Limitations of ReLU and Standard Activations
- limiting for high-frequency signals (Sharp images)
- limited expressivity for high frequencies:
	- standard activations (ReLU, tanh) struggle to capture high-frequency details and intricate textures
	- produce outputs that vary linearly
	- insufficient for complex oscillatory behaviour
- poor representation of smooth derivatives:
	- derivative of a ReLU is a constant and the derivative of a constant is 0
	- these MLPs find it hard to model signals which carry information in their derivatives
- bias toward low frequencies:
	- ReLU and similar activations tend to favour low-frequency solutions
	- challenging to capture rapid changes in signals accurately
## SIREN: Sinusoidal Representation Networks
![[SIREN, Sinusoidal Representation Networks]]
![[Screenshot 2025-11-08 at 14.31.29.png|500]]
## 3D Shapes
- INRs map $(x,y,z)$ coordinates to a scalar signal such as occupancy or distance, using a function $g: \mathbb R^3 \rightarrow \mathbb R$
	- $g(x,y,z)=d$
	- where $d$ can represent properties such as
		- [[Signed Distance Function (SDF)]]: the shortest distance from a point to the surface of the shape
		- [[Occupancy Function]]: a binary indicator for whether a point is inside or outside the shape
### Occupancy Networks and DeepSDF
- *goal*
	- both methods aim to avoid explicit, discrete representations
	- provide continuous, implicit 3D shape representations that allow higher resolution and flexibility
- *approaches*:
	- Occupancy Networks
		- learn a continuous occupancy field
		- output a probability indicating if a point is inside or outside the shape
		- suited for *tasks requiring flexible shape representation, like 3D reconstruction from sparse data*
	- DeepSDF (Signed Distance Function)
		- learn a continuous signed distance function
		- output the signed distance to the closest surface, providing detailed surface information
		- ideal for *applications needing smooth surface reconstructions with precise surface details*
## Applications
- super resolution
	- enhancing image detail by learning a continuous representation
		- INRs can represent images as continuous functions, enabling sampling at any resolution
		- for super-resolution tasks, this property allows generating high-resolution images from low-resolution inputs by sampling finer grids
	- role of network capacity
		- capacity impact: capacity of neural network directly impacts the ability to capture fine details and high-frequency information
		- higher network capacity enables the INR to model more intricate details, which is essential for realistic and sharp high-resolution inputs
		- increasing network capacity also requires careful training to avoid overfitting to low-resolution features
- Image Deblurring
	- how INRs help 
		- INRs, such as S