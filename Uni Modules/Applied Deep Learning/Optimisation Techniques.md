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
## Nesterov Accelerated Gradient (NAG)
- *Idea:* don't calculate gradient at current position since momentum will carry us forward to another position anyway - take lookahead gradient at target
	- seen as adding a 'correction term' to the standard method of momentum
	- consistently works slightly better than standard momentum in practice
- weights as follows:
$$
v_{t+1} = \alpha v_t - \eta \nabla J(X;\underbrace{W_t + \alpha v_t}_{preview \; location})
$$
- still very slow progress on shallow plateau regions
## Newton's Method
- *idea:* let curvature rescale the gradient - multiplying the gradient by the inverse Hessian leads to an optimisation that takes aggressive steps in directions of shallow curvature and shorter steps in directions of steep curvature
- *pro*: no extra learning rate or hyperparameters needed
- *con*: computing and inverting the Hessian is very expensive and space consuming (Hessian $\textbf{H}$ has square size w.r.t. number of weights)
$$
W_{t+1}=W_t - \textbf{H}(J(X;W_t))^{-1}\nabla J(X;W_t)
$$
- lots of parameters because of the hessian matrix
- inverting the big matrix is costly, in practice cannot be used
- without modifications is attracted to saddle points
## Saddle Points 
![[Screenshot 2025-09-30 at 11.17.30.png|500]]
- for an arbitrary problem, assume sign of Hessian Eigenvalues is random
	- exponentially less likely to get 'all positive' (i.e. being a minimum) with higher and higher parameter dimensions
- random matrix theory insight
	- the lower $J$ is, the more likely to find positive Eigenvalues
- neural nets without non-linearities have global minima connected via a single manifold and many saddle points
- Good:
	- most critical points with higher cost $J$ should be saddle points and they offer a chance to escape from them particularly via symmetry-breaking descent-methods
	- most local minima should therefore have a low cost $J$ associated with them and may be reachable via descent
- experiments provide some support that neural nets have as many saddle points as random matrix theory proposes
	- number of saddle points may increase exponentially with the dimensionality of the function
- bad:
	- newton's method will work poorly (since being attracted to saddle points) with a high chance of getting stuck
	- however, idea of a function-adaptive learning rate seems valuable
## Per-weight adaptive gradients
### Adagrad (adaptive gradient)
- *idea*: keep track of per-weight learning rates to force evenly spread learning speeds 
	- weights that are associated with high gradients have their effective rate of learning decreased, whilst weights that have infrequent or particularly small updates have their rates increased
	- 'monotonic learning' may help with issue including breaking of symmetries and slow progress in particular dimensions
- update now uses a $W_t$-sized accumulator $A$
$$
A_{t+1} = A_t + (\nabla J(X; W_t))^2
$$	
$$
W_{t+1} = W_t - \eta \frac{\nabla J(X;W_t)}{(\sqrt{A_{t+1}}+\varepsilon)}
$$
	- $\varepsilon$ just avoids division by 0
	- note in $A_{t+1}$ element-by-element squaring is used
- *issue*: 'monotonic learning' is a very aggressive approach and lacks the possibility of late adjustments, learning usually stops too early
### RMSprop

RMSprop you can think of $\beta$ as a forgetful parameter, as time goes on it remembers less of the previous 

- switch to SGD if ADAM can't fit in memory. SGD is always a fallback