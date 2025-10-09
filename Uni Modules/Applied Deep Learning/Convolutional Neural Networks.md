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

- Max is the most common for pooling

- backpropagation difference is now we compute all our deltas in the backward pass
- transformers use ResNet