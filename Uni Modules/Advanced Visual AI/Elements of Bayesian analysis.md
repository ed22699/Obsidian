---
tags:
  - intro
---
- $x = \theta +n, \; n \sim N(0,\sigma ^2)$
- Bayes rule: $p(\theta |x) = \frac{p(x| \theta) p(\theta)}{p(x)}$
	- where
		- $p(\theta | x)$ - posterior
		- $p(x | \theta)$ - likelihood
		- $p(\theta)$ - prior
		- $p(x)$ - evidence
- **Bayesian statistical model**: A statistical model composed of a data generation model, $p(x|\theta)$, and a prior distribution on the parameters, $p(\theta)$
- Joint distribution
	- $p(x,\theta) = p(x|\theta)p(\theta)$
- Marginal distributions
	- $p(x) = \int p(x|\theta)p(\theta)d\theta$
	- $p(\theta) = \int p(x| \theta)p(\theta)dx$

![[Bayesian estimators]]