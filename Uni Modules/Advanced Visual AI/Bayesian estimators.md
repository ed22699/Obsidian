---
tags:
  - intro
---
- A Bayesian estimator minimises the conditional risk, which is the loss (cost function) averaged over the conditional (posterior) distribution of $\theta$, given the observation (measurement) x
$$
\hat \theta (x) = \arg _\theta \min \int C[\theta, \hat \theta (x)]p(\theta|x)d\theta
$$
- The *Bayes risk R* is the average cost $E[C(\varepsilon)]$ and measures the performance of a given estimator
	- $R = E[C(\varepsilon)]$ 