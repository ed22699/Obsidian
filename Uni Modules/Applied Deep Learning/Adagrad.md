---
tags:
  - optimisation
---

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