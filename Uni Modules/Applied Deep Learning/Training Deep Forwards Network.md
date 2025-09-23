---
tags:
  - Lesson
---
- Problem
	- highly non-linear function, the cost function $J$ of a network, and we want to find a parameterisation $W$ across all weights $w_{ij}^l$ that minimises it
![[Screenshot 2025-09-23 at 16.00.46.png|400]]
![[Screenshot 2025-09-23 at 16.01.05.png|400]]
- we require: $\nabla J(X;W) = \nabla J_X(W)$ as given by all $\frac{\delta J_X(W)}{\delta w_{ij}^l}$
	- where $w_{ij}^l$ is the $i^{th}$ weight to the $j^{th}$ neuron of the $l^{th}$ layer. Thus, we need to compute partial derivatives of $J$ w.r.t. all weights
## Potential Options for Calculating Error Derivatives
- Symbolic Differentiation
	- not supporting arbitrary setups
	- solution structure may not resemble network structure at all
- Numerical differentiation (find the lowest gradient at that point and go that way)
	- trivial to implement 
	- low accuracy
	- potentially high computational cost
- automatic differentiation of the network's computational graph
	- used by Tensorflow
## Relationships in Feedfoward Computational Graphs
- how do we differentiate this?
	1. Differentiate everything (long, not fun)
	2. chain rule and summing over all paths (based on network layout)
		- observe how many paths between $f$ to $a$
		- the influence of $f$ over $a$ is the sum of all these connected paths derivatives, for that we can use the chain rule
		![[Screenshot 2025-09-23 at 15.40.44.png|500]]
		- problem is this is very big in some deep networks, every neuron impacts the next layer, not fun differentiation	
	3. Observe the hierarchical dependency 
		- once you know the derivatives associated to the layer above, summation of them from connected nots times local derivatives is sufficient to get the next layer of derivatives
		- propagate backwards
		![[Screenshot 2025-09-23 at 15.46.09.png|500]]

- two-pass strategy
	- forward pass to give values to nodes and output
	- backward pass to establish deltas $\delta$, i.e. all partial derivatives
- requirements
	- feed-forward network
	- local per-edge derivatives must be known
- solution tactic
	- instead of explicit summation over all paths, layer-by-layer evaluation via summation over all incoming local derivatives times their associated deltas
![[Screenshot 2025-09-23 at 16.08.11.png|500]]