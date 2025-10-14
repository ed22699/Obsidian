---
tags:
  - Lesson
---

- Most important thing to tune is the learning rate, if you can only tune one thing tune this
![[Drawing 2025-10-14 17.38.34.excalidraw|700]]
- *batch size*: 
	- basic concept is bigger is better
	- powers of 2 are common
	- in practice there usually is an optimal batch size which isn't everything
- *init weights*:
	- using pre-trained is just better
		- try to find something of a similar focus 
		- for images ImageNet is sometimes used
- *Freezing weights*:
	- can just train the final few layers of a network if the model is too big to train/store in memory
		- freeze part of the network so gradient is blocked and doesn't pass through, you basically just stop backpropagation where the freeze is
		- typically freeze early parts of the network
		- can freeze last few layers to help training
- *batch normalisation*:
	$$
	\hat x = \frac {x-\bar x}{\sigma}
	$$
	- standardising features over all dimensions is non-differentiable
	- instead do per dimension
	$$
	\hat x_j = \frac {x_i - \bar x_i}{\sigma _i + \epsilon}
	$$
	- changes what the layer can represent
		- therefore apply a pair of parameters $\gamma$ and $\beta$ to scale the inputs to the next layer
		$$
		y = \gamma \hat x +\beta
		$$
	- in practice we keep a moving average of the mean/std which is then used during testing