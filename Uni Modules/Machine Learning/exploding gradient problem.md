---
tags:
  - training
---
A very Large Gradient
# Solutions
## Gradient clipping
- if gradient too big can use gradient clipping
- can be used to cap the magnitude of the gradient
- original gradient $\boldsymbol{g}$ and the clopped gradient $\boldsymbol{g}'$ are related as follows: $\boldsymbol{g}'=min(1,\frac{c}{||\boldsymbol{g}||})\boldsymbol{g}$ 
> [!note]
> $\boldsymbol{g}'$ points in the same direction as $\boldsymbol{g}$

## Non-saturating activation functions for deep learning
- sigmoid activation function, for example, saturates at large negative or lager positive values
![[Screenshot 2024-09-25 at 09.18.19.png|500]]
- its gradient there will be $0$ preventing gradient descent from reaching good weights
- **solution**: choose activation functions that don't saturate
	- ReLU and its variants are popular choices. 
		- note plain ReLU has zero gradient for negative values so might end up with the 'dead ReLU' problem
		- note also that ReLU is not a differentiable function at 0, but we can just impose a derivative value of 0 there