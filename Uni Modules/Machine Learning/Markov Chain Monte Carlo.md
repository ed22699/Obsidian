---
tags:
  - Lesson
  - markov_chain_monete_carlo
---
## Bayesian approach
- goal is to compute the posterior distribution $P(\theta|D=d)$ where $\theta$ is the parameter vector and $d$ is the observed value of the data
- we choose a prior $P(\theta)$ and assume a particular likelihood $P(D|\theta)$ and then [[Bayes theorem]] gives us $P(\theta|D=d)\propto P(\theta)P(D=d|\theta)$ 
- if we choose a conjugate prior for $P(\theta)$, then representing and computing $P(\theta|D=d)$ is easy 
### Problems
- for most probabilistic models of practical interest, exact inference is intractable, and so we have to resort to some form of approximation
- we want to be able to 
	- construct whatever joint distribution $P(\theta,D)$ we think best models the data-generating process
	- compute $P(\theta|D=d)$
- with this flexibility we may not be able to represent or compute $P(\theta|D=d)$ easily
- solution:
	- give up on getting $P(\theta|D=d)$ exactly
	- draw samples ([[univariate sampling]]) of $\theta$ from $P(\theta|D=d)$ which will allow us to approximately compute any posterior quantities (e.g. mean of $P(\theta|D=d)$) 
		- often we want to compute expected values with respect to some posterior distribution $E[f]=\int f(\boldsymbol{z})p(\boldsymbol{z})d\boldsymbol{z}$ 
		- if we draw independent samples $\boldsymbol{z}^{(I)}, I=1,...,L$ from $p(\boldsymbol{z})$ then we can approximate $E[f]$ with $\hat{f}=\frac 1L\sum_{l=1}^Lf(\boldsymbol{z}^{(l)})$ 
# Markov chain Monte Carlo
- if we can sample from a distribution then we have a simple way to compute approximate values, however if we cannot then:
	- if we can sample from a sequence of distributions which eventually reaches (or get very close to) the desired distribution, then we can adopt the MCMC strategy:
		1. draw a sample from each distribution in this sequence
		2. only keep the sample once we get 'close enough' to the desired distribution
- the goal of MCMC is to design a [[Markov Chain]] so that the sequence of marginal distributions converges on the distribution we want
- we can just sample from the [[Markov Chain]] and only keep the sampled values of the later random variables
	- sampled values we draw are **not** independent (reducing the quality of the approximations we end up with), but this is a price we have to pay
## how MCMC works
- aim: given a target probability distribution $p(\boldsymbol{z})$, construct a Markov chain $\boldsymbol{z}^{(1)},...,\boldsymbol{z}^{(i)},...$ such that $\lim _{i \to \infty}p(\boldsymbol{z}^{(i)})=p(\boldsymbol{z})$ 
	- for Bayesian machine learning the target distribution will be $P(\theta|D=d)$, the posterior distribution of the model parameters given the observed data
	- one solution to this is the [[Metropolis-Hastings algorithm]]
	- probabilistic programming systems like PyMC uses more sophisticated MCMC algorithms to avoid getting stuck
- for MCMC we:
	1. throw away early samples (burn-in)
	2. run independent chains to check for convergence
# Reading
- bishop 11.1.2
- bishop 11.2