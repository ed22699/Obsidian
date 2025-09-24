---
tags:
  - theoretical_peliminaries
---
- regularisers are non-smooth, so gradient descent doesn't work well
- proximal splitting provides the numerical algorithms to actually compute the solution when priors/regularisers are complex
- proximal splitting methods such as ADMM split the problem into a data term (smooth, quadratic) and a regulariser (possible non-smooth)
	- this is used to handle the regulariser efficiently
- many MAP problems can be solved by iterating between
	- gradient descent step on the likelihood
	- proximal step of the prior
## Iterative Optimisers
- MAP estimation is an optimisation problem of the form 
$$\hat x_{MAP} = \arg \min [l(y,x)+ \lambda p(x)]$$
- Alternate Direction of Multipliers Method (*ADMM*) involves variable splitting
$$
\{\hat x_{MAP}, \hat v\} = \arg \min [l(y,x)+\lambda p(v)] \; s.t. \; x=v
$$
- through the augmented Lagrangian method, the constrained becomes a penalty term
$$
\{\hat x_{MAP}, \hat v\} = \arg \min [l(y,x)+\lambda p(v) + \frac \beta 2 ||x-v+u||_2^2]
$$
- when we split x into x and v it means we can minimise both parameters separately
1. Update of x:
	- $\hat x= \arg \min [l(y,x)+\frac \beta 2 ||x-v+u||_2^2]$
	- the above is now an $L_2$ regularisation
2. Update of v:
	- $\hat v= \arg \min [\lambda p(v) + \frac \beta 2 ||x-v+u||_2^2]$
	- this is a denoising of the image $x+u$, assumed to be contaminated with AWGN of power $\sigma^2 = 1/\beta$
3. Update of u:
	- $\hat u = u + x-v$

