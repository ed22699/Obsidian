---
tags:
  - Lesson
  - k-means_gaussians
---
# K-means
![[Screenshot 2024-10-15 at 11.02.04.png|300]]
1. select random means
2. split data upon those means
3. recalculate the means of those clusters
4. repeat 2-3 until minimal movement in clusters means

- $r_{nk}=1$ if datapoint $\boldsymbol{x}_n$ is assigned to cluster $k$
	- $r_{nk} = \begin{cases}1 & \text{if } k=\arg\min_j||\boldsymbol{x_n=\boldsymbol{\mu}_j}||^2\\0 & \text{otherwise} \end{cases}$ 
- $\boldsymbol{\mu}_k$ is the mean of cluster $k$
	- $\boldsymbol{\mu}_k=\frac{\sum_n r_{nk}\boldsymbol{x}_n}{\sum_n r_{nk}}$ 
# Gaussian mixture distribution
- groups by ellipses
- more complex than k-means (more parameters)
![[Screenshot 2024-10-14 at 09.37.12.png|300]]
$$
p(\boldsymbol{x})=\sum_{k=1}^K\pi_k\mathcal{N}(\boldsymbol{x}|\mu_k, \Sigma_k)
$$
- we can associate the mixing coefficients $\pi_k$ with a $K$-dimensional random variable $\boldsymbol{x}$ where:
	- $z_k \in \{0,1\}$
	- $\sum_kz_k=1$
	- $p(z_k=1)=\pi_k$
	- so $p(\boldsymbol{x})=\sum_{\boldsymbol{z}}p(\boldsymbol{z})p(\boldsymbol{x}|\boldsymbol{z}) = \sum_{k=1}^K\pi_k\mathcal{N}(\boldsymbol{x}|\mu_k, \Sigma_k)$
- with a full joint distribution $p(\boldsymbol{x}, \boldsymbol{z})$ we can define the responsibility that component $k$ has for explaining observation $\boldsymbol{x}$
	- $\gamma(z_k)=p(z_k=1|\boldsymbol{x})$
- to sample from a Gaussian mixture just use ancestral sampling (sample from $p(\boldsymbol{x})$ and then from $p(\boldsymbol{x}|\boldsymbol{z})$)
- if we want we can put restrictions on the covariance matrices of the Gaussians in the mixture
## Soft clustering with Gaussian mixtures
- the overlap areas where the probability of either option is roughly equal does not decide on a single option but instead shows there is multiple possible outcomes
![[Screenshot 2024-10-14 at 09.31.39.png|400]]
- given data $\boldsymbol{X}$ and a fixed number $K$ of component Gaussians, we can use MLE ([[Maximum Likelihood Estimation]]) to get a particular Gaussian mixture distribution
	- gives soft clustering
	- log-likelihood: 
	$$
	\ln p(\boldsymbol{X}|\boldsymbol{\pi}, \boldsymbol{\mu}, \boldsymbol{\Sigma})=\sum_{n=1}^N\ln\{\sum_{k=1}^K\pi_k\mathcal{N}(\boldsymbol{x}_n|\boldsymbol{\mu}_k,\boldsymbol{\Sigma}_k\}
	$$
	- problems:
		- possible singularities
		- symmetry/non-identifiability
		- no closed form for the MLE
	- Solution: [[EM algorithm]]
		- 
# Reading
- bishop 9.1 (skip 9.1.1 but interesting)
- bishop 9.2 up to 9.2.1
