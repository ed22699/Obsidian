---
tags:
  - optimisation
---

- *Idea:* don't calculate gradient at current position since momentum will carry us forward to another position anyway - take lookahead gradient at target
	- seen as adding a 'correction term' to the standard method of momentum
	- consistently works slightly better than standard momentum in practice
- weights as follows:
$$
v_{t+1} = \alpha v_t - \eta \nabla J(X;\underbrace{W_t + \alpha v_t}_{preview \; location})
$$
- still very slow progress on shallow plateau regions