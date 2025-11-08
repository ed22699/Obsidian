---
tags:
  - Lesson
---
- taking image and turning it into a 3D model
# Discrete Representations
- existing 3D representations discretise the output space differently
	- spatially in voxel representations
	- in terms of predicted points
	- in terms of vertices for mesh representations
## Limitations of Discrete Representations
- Resolution limitations
	- *fixed grid resolution* limits detail, requiring significantly more memory to increase fidelity
	- *fine details and smooth surfaces are difficult to capture*, leading to blocky or jagged artefacts
- memory inefficiency
	- *exponential memory growth* in 3D as resolution increases
	- many *regions in 3D spaces are sparse*, wasting memory in empty areas
- lack of flexibility 
	- fixed resolution across the entire shape, unable to dynamically adjust detail
	- real-world shapes are inherently continuous, making discrete grids unnatural for detailed representations
- computational inefficiency 
	- operations on large grids are computationally expensive
	- scaling to high resolution becomes infeasible for real-time applications
# Implicit Representation
- offer a flexible approach to 3D modelling, avoiding discretisation limitations
- support arbitrary topology and resolution, enabling detailed and complex shapes without fixed structures
- *Issue*: Given a complex signal, finding an exact function $f$ that represents it continuously is challenging
	- such functions are often "too complex to simply write them down"
- *Solution*: Implicit neural representations
	- neural networks (e.g. MLPs) are used to estimate this function $f$
	- trained on discrete samples of a signal, neural networks learn to approximate the continuous function $f$, denoted as $\mathcal F$ 
- network parameterises $\mathcal F$, with $f$ implicitly encoded in the network after training - hence the term *Implicit Neural Representation*
## Mappings in 2D (Images)
- for an image, INRs learn a function $f: \mathbb R^2 \rightarrow \mathbb R^3$ that maps each spatial coordinate $(x,y)$ to an RGB colour value
	- $f(x,y) = \begin{bmatrix}R \\ G \\ B \end{bmatrix}$
	- where $f(x,y)$ outputs the red, green and blue values for each pixel coordinate $(x,y)$
## Implicit Neural Representation Model
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