---
tags:
  - model_based_deep
---
$$
y = Hx + n, n\sim N(0,\sigma ^2 I)
$$
$$
\hat x_{MAP} = \arg\min_{\hat x} [l(y,x) + \lambda \varphi (x)]
$$
$$
\hat x = \arg \min_{\hat x}(\frac 1 2 ||y-Hx||_2^2 + \lambda \varphi (x))
$$
$$
\hat x _{LASSO} = \arg \min_{\hat x}(\frac 1 2 ||y -Hx||_2^2 + \lambda||x||_1)
$$
$$
\nabla l(x) = -H^T(y-Hx)
$$
- proximal mapping is given by
$$
prox_{\mu \varphi}(v) = \arg \min_{u}(||u-v||_2^2 +\frac \lambda \mu ||u||_1) = S_{\mu \lambda}(v)
$$
- $S_\lambda$ is soft thresholding operator
$$
S_\lambda (x) = sign(x)\max\{0, |x| - \lambda\}
$$
- ISTA is the formulation of the resulting proximal gradient descent method, and its update equation is given by
- **stopped notes here**
---
$$
x^{l+1} = S_\lambda \{x^l+\frac 1 \mu H^T \} 
$$
## Learned ISTA (LISTA)
- the block on the right a single network layer does what the left does but with learning