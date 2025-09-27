---
tags:
  - Lesson
---
- Concept
	- combine *reverse auto-differentiation* (for finding relationship of cost function to each weight) with *gradient descent* (for stepwise adjustment of weights)
- intuition behind Error Derivative Propagation
	- compute discrepancy between network output and target
	- propagate this discrepancy backwards through the network adjusted by the influence of the paths travelled in order to determine the influence of each and every weight (ends of paths) towards the discrepancy
## Overall Strategy
- calculate neuron activities for all layers and cost in a forward pass given the input
- at the top of the network, convert the discrepancy between outputs and targets according to the cost function into error derivatives linked to the final layer output (the topmost deltas)
- layer by layer, calculate error derivatives for neurons in hidden layers by combining all connected error derivatives in the layer above and considering the effect of activation functions - thereby, propagating error derivatives backwards
- use neuron activities to get error derivatives w.r.t. the weights
![[Screenshot 2025-09-23 at 16.29.34.png|300]]
### Backpropagation: Step 1
- calculate all $s_j^l$ and $f_j^l$ in a single forward pass
- at the top of the network, convert the discrepancy between outputs $f^N$ and targets $f^*$ into error derivatives $\delta _j^{N+1}$ linked to all final layer neurons $j$ according to $J$, and compute $\delta _j ^N$
![[Screenshot 2025-09-27 at 12.47.11.png|200]]
![[Screenshot 2025-09-27 at 12.48.11.png|500]]
### Backpropagation: Step 2
- layer by layer, calculate all error derivatives $\delta _i ^{l-1}$ in each hidden layer from all error derivatives $\delta _j^l$ in the layer above
![[Screenshot 2025-09-27 at 12.49.50.png|300]]
### Backpropagation: Step 3
- use these error derivatives $\delta _j ^l$ w.r.t. activities $f_i^{l-1}$ to get error derivatives w.r.t. the weights
![[Screenshot 2025-09-27 at 12.52.40.png|200]]
## The Algorithm
![[Screenshot 2025-09-27 at 12.53.26.png|500]]
- initialise all weights randomly
	- make sure its not 0, good to be a normal distribution around 0 for the weights
	- best starting weights is someone else's from a similar model that has already been trained
- three important things that are hard to decide
	- initialisation
	- learning rate
	- stopping criteria
- backpropagation has been known since 1970s
- what stood in the way of training deep nets effectively?
	- fundamental issue of gradient instability when training truly deep architectures: originally known as the *vanishing gradient problem* since 1990s
		- we need fast, differentiable and meaningful robust neuron layouts to address this issue (e.g. ReLU LSTM)
	- descent-based optimisation techniques *need to work accurately and fast in practice despite large training data sets* (GPU parallelisation and improved optimisers help a lot here)
	- *number of parameters explode in deep networks*; we may need to share them or reuse the entire net (e.g. CNNs/RNNs)
	- regularisation techniques are critical to achieve good generalisation beyond the training data available
## Activation Functions
![[Screenshot 2025-09-27 at 12.59.48.png|500]]
### Vanishing Gradient Problem
![[Vanishing Gradient Problem]]
## Rectifying Linear Unit (ReLU)
- combines high speed of evaluation with a non-saturation non-linearity 
- combined effect may yield practically 5-10 times faster convergence of a network
- however, it introduces a new problem a.k.a *Dying Neurons*
	- a large gradient flowing through a ReLU unit may force the neuron to never activate again (with the incoming signal always averaging under zero)
	- network may end up carrying a lot of dead units that will not contribute to learning anymore
![[Screenshot 2025-09-27 at 13.15.17.png|400]]
### The Dying Neuron Problem
![[The Dying Neuron Problem]]
- avoid using sigmoids and expect $\tanh$ to work worse than ReLU
- as a current standard use ReLU as activation function: you ay need to control the learning rate (set fairly low) and monitor the fraction of dead units
- leaky versions or generalisations of ReLU may help combat dying neurons
	- leaky ReLU is not as fast as ReLU
		- only really use the leaky ReLU when you have a model thats particularly hard to train
- many more activation functions have been proposed
![[Screenshot 2025-09-27 at 13.31.19.png|700]]