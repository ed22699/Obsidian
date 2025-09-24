---
tags:
  - theoretical_peliminaries
---
$$
y = Hx + n, n \sim N (0, \sigma ^2 I)
$$
- $H$ is the degradation matrix, which is assumed to be block-circulant and $n$ is AWGN
- Bayesian formulation
	- $\hat x _{MAP} = \arg\max [\ln p(y|x) + \ln p(x)]$
	- $= \arg \min [- \ln p (y|x) - \ln p(x)]$
		- rewrite the log-likelihood term as $l(y,y)= - \ln p(y|x)$
		- rewrite the prior term as $\lambda p(x) = -\ln p(x)$
		- hence the variational formulation is:
			$$\hat x_{MAP} = \arg \min [l(y,x)+ \lambda p(x)]$$
![[Constrained Least-squares]]
![[Proximal Splitting]]