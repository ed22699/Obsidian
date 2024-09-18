---
tags:
  - Regression_and_Discriminant
---

- probabilistic model parameters need to be tuned/trained
- MLE is a method of estimating the parameters of a probabilistic model
- assume $\theta$ is a vector of all parameters of the probabilistic model 
	- e.g. $\theta = \{a_{1}, \sigma\}$ 
- MLE is an extremum estimator (estimator calculated through maximisation of a certain objective function) obtained by maximising an objective function of $\theta$ 
- Assume $f(\theta)$ is an objective function to be optimised and arg max corresponds to the value of $\theta$ that attains the maximum value of the objective function $f$
	- $\hat{\theta} = arg$ $max_{\theta}f(\theta)$ 
## MLE Recipe
1. Determine $\theta$, $D$ and expression for likelihood $p(D|\theta)$
	- $\theta_{MLE} = arg$ $max_{\theta}p(D|\theta)$
2. Take the natural logarithm of the likelihood
	- $= arg$ $max_{\theta}\ln p(D|\theta)$
3. Take the derivative of $\ln p(D|\theta)$ w.r.t. $\theta$. If $\theta$ is a multi-dimensional vector, take partial derivatives
	- $= arg$ $min_{\theta}-\ln p(D|\theta)$
4. Set derivatives to $0$ and solve for $\theta$
- in the case of standard linear regression the parameters which minimise the squared error are also the MLE parameters
- in general this recipe will only find local maxima of the likelihood (not necessarily the MLE), this is due to the fact that there could be another lower dip later on and the function is stuck in the higher
## [[Logistic Regression - Maximum Likelihood Estimation recipe]]