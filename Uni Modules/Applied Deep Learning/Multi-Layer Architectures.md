---
tags:
  - basic_neural
---
![[Screenshot 2025-09-27 at 12.28.17.png|500]]
- $\underbrace{f^N}_{output \; layer} = f^{\overbrace{N}^{depth}}(...f^2(f^1(\underbrace{f^0}_{input \; layer} ; W^1); W^2)...;W^N)$
- $\underbrace{\textbf W}_{all \; parameters} = [W^1W^2...W^N]= \begin{bmatrix}... && ... && ... \\ ... && w_{ij}^l && ... \\ .. && ... && ... \end{bmatrix}$
	- weight $w_{ij}^l$ connects the $i^{th}$ neuron in layer $l-1$ to the $j^{th}$ neuron in layer $l$
### Learning Representations
- basic *perceptron* represent a *linear classifier*
- *boolean functions* can be represented by layered networks with *one hidden layer* (networks may be very wide requiring an exponential number of hidden neurons compared to input)
- layered networks with *one hidden layer* can also represent *any continuous function*
- layered networks with *two hidden layers* can represent *any mathematical function*
- why do we deep advantageous at all?
![[Screenshot 2025-09-27 at 12.40.45.png|500]]
![[Screenshot 2025-09-27 at 12.41.31.png|500]]