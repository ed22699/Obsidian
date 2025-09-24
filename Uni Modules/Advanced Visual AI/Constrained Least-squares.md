---
tags:
  - theoretical_peliminaries
---
- this is a way regularising using [[Bayesian (MAP) and variational frameworks duality]]
## Explicit Solvers
- regularisation technique which consists in choosing the $x$ that minimises the Lagrangian:
	$$
	\hat x = \arg \min (||y - Hx||^2 + \lambda ||Cx||^2)
	$$
	- $\lambda$ represents either a Langrangian multiplier or a fixed parameter called a *regularisation parameter*
	- $\lambda$ controls the relative contribution between the data attachment term $||y -Hx||^2$ and the prior term $||Cx||^2$
- taking the derivative of the Lagrangian we get $-2H^T(y - Hx)+2\lambda C^T Cx$
- setting the above to zero we get:
	$$
	\hat x = (H^T H +\lambda C ^T C)^{-1}H^Ty
	$$
	- large values of $\lambda$ lead to more regularisation
		- drawback: restored image will contain more ringing
	- small values of $\lambda$ will result in less reduction of the noise effects
