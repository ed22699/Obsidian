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
$$
x^{l+1} = S_\lambda \{x^l+\frac 1 \mu H^T (y-Hx^l)\} 
$$
or
$$
x^{l+1} = S_\lambda \{(l-\frac 1 \mu H^T H)x^l+\frac 1 \mu H^T y\} 
$$

## Learned ISTA (LISTA)
![[Screenshot 2025-10-08 at 09.08.56.png|500]]
- the block on the right a single network layer does what the left does but with learning
- to unroll ISTA, the iteration can be recast into a single network layer
- Executing ISTA L times can be interpreted as cascading L network layers - that forms a L-layer deep neural network
- the generic forward operator $H$ has been replaced with $W$, to symbolise the learnable nature of the matrix, which might also not necessarily be known exactly
- in the unrolled network an implicit substitution of parameters has been made as:
$$
W_t=l -\frac 1 \mu W^T W
$$
and
$$
W_e = \frac 1 \mu W^T
$$
- after unrolling ISTA into LISTA, the network is trained via back-propagation in order to optimise the parameters $W_t$, $W_e$ and $\lambda$
- training is performed in a supervised manner, i.e. for every input vector $y^t, t=1,...,T$ its corresponding output $x^{*t}$ is known
- the training loss function is formed by comparing the predicted output $\hat x (y^t;W_t,W_e,\lambda)$ with ground truth $x^{*t}$
$$
l(W_t,W_e,\lambda) = \frac 1 T \sum _{t-1}^T ||\hat x(y^t;W_t,W_e,\lambda)-x^{*t}||^2_2
$$
- LISTA may achieve higher efficiency than ISTA
- LISTA is useful when $W$ is hard to determine
- the number of layers $L$ in (trained) LISTA can be an order of magnitude smaller than the number of iterations required for ISTA to achieve convergence
