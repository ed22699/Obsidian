---
tags:
  - Lesson
---
- bad idea to take one sample at a time OGD (Online gradient descent) - lead to very noisy gradient descent
- DGD (deterministic gradient descent) is the opposite extreme
	- difficult because
		- limited memory on the GPU
		- may overfit if it is seeing everything all at once. Want to fit to the class not the data
- Middle ground is SGD (Stochastic gradient descent)
	- the standard algorithm at the moment 
![[Screenshot 2025-09-29 at 16.13.09.png|500]]
### SGD with 'Simulated Annealing'
- introduce a changing learning rate $\eta _k$ decreasing over $\tau + l$ steps by blending from a starting learning rate $\eta _0$ towards a final learning rate $\eta _\tau$ 
![[Screenshot 2025-09-29 at 16.19.38.png|500]]
- basically big jumps to get roughly near slowly turning into little jumps as you get closer
- *Issue*: still can get trapped in very localised, shallow 'dips' when using DGD given very small learning rates. 
	- aim to surf over these local depressions on steep hills
## Momentum
![[Screenshot 2025-09-29 at 16.24.49.png|300]]
- *Idea*: introduce a velocity term $v$ of 'current descent speed' and use current gradient to change this velocity rather than weights directly
	- step sizes now depend on how large and how aligned a previous sequence of gradients have been
	- change the update equations for weights from: $W_{t + 1} = W_t - \eta \nabla J(X;W_t)$ 
		- by introducing velocity accumulation
$$
v_{t+1} = \underbrace{\alpha}_{momentum \; parameter} v_t - \eta \nabla J(X;W_t)
$$
$$
W_{t+1} = W_t + \underbrace{v_{t+1}}_{momentum}
$$
- **gave up notes here**
-----------------------
## Nesterov Accelerated Gradient (NAG)
$$
v_{t+1} = \alpha v_t - \eta \nabla J(X;\underbrace{W_t + \alpha v_t}_{preview \; location})
$$
- lots of parameters because of the hessian matrix
- inverting the big matrix is costly, in practice cannot be used


RMSprop you can think of $\beta$ as a forgetful parameter, as time goes on it remembers less of the previous 

- switch to SGD if ADAM can't fit in memory. SGD is always a fallback