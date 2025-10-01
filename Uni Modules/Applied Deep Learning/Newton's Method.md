---
tags:
  - optimisation
---

- *idea:* let curvature rescale the gradient - multiplying the gradient by the inverse Hessian leads to an optimisation that takes aggressive steps in directions of shallow curvature and shorter steps in directions of steep curvature
- *pro*: no extra learning rate or hyperparameters needed
- *con*: computing and inverting the Hessian is very expensive and space consuming (Hessian $\textbf{H}$ has square size w.r.t. number of weights)
$$
W_{t+1}=W_t - \textbf{H}(J(X;W_t))^{-1}\nabla J(X;W_t)
$$
- lots of parameters because of the hessian matrix
- inverting the big matrix is costly, in practice cannot be used
- without modifications is attracted to saddle points