---
tags:
  - Lesson
---

## Issues with Fully Connected Networks
- issue of scale
	- will be costly to train as dimensions and weights to learn can blow up very quickly, 
		- e.g. a 224x224 px image with 3 colour channels has 150,528 input dimensions. If we have 10 output classes, with one layer this is 1,505,280 weights to learn
- given a couple sentences
	- in a fully connected layer, multiple neurons have to learn the words in different positions
		- we want a network that is *translationally invariant*
- given a repeating signal 
	- there are some local dependencies 
	- we want to treat similar inputs the same
- *solutions*: 
	- only connect neighbours
		- we go from $O(n^2)$ to $O(n)$
		- only capture local dependencies
		- this is still quite a lot of weights
	- share weights between different pairs of neurons
		- everything the same colour has the same weight
		- do the same for other connections as well
		- $O(1)$ regardless of input size
		- does not reduce the runtime of the forward pass
			- still the same number of calculations
		- memory required for the model is much *smaller*
		- significantly *less parameters* to train = *less data required*
		- caveat of assuming that your *data is grid-like*
![[Screenshot 2025-10-08 at 16.30.30.png|400]]
![[Screenshot 2025-10-08 at 16.31.27.png|400]]
- using only the neighbouring weights is limiting learning
- *solution*: add ore layers until we cover more output neurons
- neuron's influence is known as the *receptive field*
	- shown in the image below for forwards pass and backpropagation 
![[Screenshot 2025-10-08 at 16.33.15.png|400]]
![[Screenshot 2025-10-08 at 16.34.13.png|200]]
- this is effectively cross-correlation
$$
(f*w)(i)=\sum _{j=-1}^1 f(i)w(i+j)
$$
> [!note]
Convolution is lightly different: $(f*w)(i)=\sum_{j=-1}^1 f(i)w(i-j)$
- kernel is flipped in all dimensions
- convolution has the commutative property: $f*w=w*f$
	- this doesn't hold for cross-correlation
	- in practice, most DL libraries use cross-correlation 
## Convolution
- padding
	- adding blank rows/columns so that the output image doesn't shrink
- stride
	- how much we move the kernel each step
	- stride 2 allows for a larger *receptive field*
	- a larger stride *down-samples* your feature
### Convolutional Layers
- if we learn a single kernel per layer - too few weights
	- even with a 11x11 kernel, only 121 weights per layer
	- *solution*: stack kernels
		- output increases in dimensions
		- with multiple kernels, each can now specialise
- for images we have 3 dimensions
	- usually denoted Height, Width and Depth
	- as our input is 3D, we actually perform a 3D convolution operation
		- in this case 2D refers to how the kernel is shifted through the image
		![[Screenshot 2025-10-13 at 15.11.35.png|400]]
- activation functions? $f_i^{l+1} = g(f_i^l * w_{j,i}^l)$
	- we just apply the activation function on the output
![[Screenshot 2025-10-13 at 15.14.51.png|400]]
## Pooling
- as the size of our inputs are huge compared to our kernels, after multiple layers we still have huge input features
- pooling reduces your input size by applying a downscaling function
	- Max is the most common function for pooling
	- other functions are available
		- average, weighted average, L2 norm
![[Screenshot 2025-10-13 at 15.17.50.png|100]]
- pooling allows for small translational invariance
	- in addition to CNN Kernels also providing this
- further increases the receptive field
## CNN Architecture Design 
- CNN Layers and Pooling layers are alternated
	- increases receptive field of each neuron
- after CNN Layers and Pooling, we might be left with
	- if we're performing classification, we have $n$ classes
	- solution: reshape, and add one (or more) FC (fully connected) Layers
![[Screenshot 2025-10-13 at 15.23.39.png|400]]
![[Screenshot 2025-10-13 at 15.23.54.png|400]]
![[Screenshot 2025-10-13 at 15.24.15.png|400]]
## Training CNNs
![[Screenshot 2025-10-13 at 15.24.47.png|400]]
### Auto-Differentiation for CNNs
- each weight now has impact on many different output nodes
![[Screenshot 2025-10-13 at 15.26.23.png|300]]
- still need to know local per-edge derivatives
	- solution: sum all incoming local derivatives multiplied by their associated deltas
		- i.e. accumulate gradients
![[Screenshot 2025-10-13 at 15.28.41.png|400]]
- increasing layer sizes
	- as always in Deep Learning, Models get deeper
	- vanishing gradients are still an issue in CNNs
	- FC layers are easy to train - small size and near the output
- backpropagation difference is now we compute all our deltas in the backward pass
## ResNet
![[Screenshot 2025-10-13 at 15.30.36.png|300]]
- faster/easier convergence
- the output is dominated by the residual (original) input, therefore only slight differences are learnt
- layers are constructed as identity mappings as a starting point, and almost acting as regularisation
![[Screenshot 2025-10-13 at 15.32.31.png|400]]
- transformers use ResNet
## ResNeXt
![[Screenshot 2025-10-13 at 15.33.17.png|400]]
![[Screenshot 2025-10-13 at 15.33.32.png|400]]
## 1x1 Convolutions
- can be thought of as a weighted pooling along the *depth* dimension