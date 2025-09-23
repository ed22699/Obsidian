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




- initialise all weights randomly
	- make sure its not 0, good to be a normal distribution around 0 for the weights
	- best starting weights is someone else's from a similar model that has already been trained

- three important things that are hard to decide
	- initialisation
	- learning rate
	- stopping criteria

- leaky ReLU is not as fast as ReLU
	- only really use the leaky ReLU when you have a model thats particularly hard to train