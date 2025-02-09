---
tags:
  - Lesson
  - transforms
---
## Variance Stabilising Transforms
- usual assumption in regression is that the variance of each observation is the same
	- problem: in many cases, the variance is not constant, but is related to the mean
		- Poisson data (counts of events): $\mathbb E (X) = Var(X)=\mu$ 
		- Binomial data (and percents): $\mathbb E (X) = m \pi , \; Var(X) = m\pi (1 - \pi)$ 
		- General Case: $\mathbb E (X) = \mu, \; Var (X) = f(\mu)$
		- Power relationship: $Var(X) = \sigma ^2 = \alpha ^2 \mu ^{2\beta}$ 
		$$\sigma = \alpha \mu ^\beta \Rightarrow \log(\sigma) = \log (\alpha) + \beta \log (\mu)$$
- Box-Cox transformation can be used to diagnose and transform
## Decorrelating
![[Screenshot 2025-02-09 at 11.43.35.png|500]]
- transform data so that it has diagonal covariance matrix $\Sigma = X^TX$
	- This transform can be found by solving an eigenvalue problem: $\Sigma \Phi = \Phi \Lambda$, where $\Lambda$ is a diagonal matrix of eigenvalues, and the columns of $\Phi$ are the eigenvectors of the covariance matrix
	- $\Phi$ diagonalises $\Sigma$ 
	- diagonalised covariance can also be written as: 
		$$\Phi ^T \Sigma \Phi = \Lambda \tag{1}$$
	- so to de-correlate a single vector $x_i$ we do: 
		$$\hat x_i = \Phi ^T x_i \tag{2}$$
## Whitening data 
![[Screenshot 2025-02-09 at 11.51.30.png|400]]
- the diagonal elements (eigenvalues) in $\Lambda$ may be the same or different
- if we make them all the same, then this is called *whitening* the data
- each eigenvalue determines the length of its associated eigenvector
	- not whitened $\Rightarrow$ elliptical $\Sigma$
	- Whitened $\Rightarrow$ spherical $\Sigma$ 
- $\Lambda ^{-1/2}\Lambda \Lambda ^{-1/2} = I$
	- $\Lambda^{-1/2}\Phi ^T \Sigma \Phi \Lambda ^{-1/2} = I$
- to apply to $\hat x_i$ multiply by this scale factor $\rightarrow$ whitened data point $\tilde x_i$:
	$$\tilde x_i = \Lambda ^{-1/2}\hat x_i = \Lambda ^{-1/2} \Phi ^T x_i
	\tag{3}$$
	- now $\Sigma$ is not only diagonal, but also uniform (white), singe $\mathbb E (\tilde x_i \tilde x_i^T) = I$ 
### When this might not be useful
1. the scaling of data examples is somehow important in the inference problem you are looking at 
	- could use the eigenvalues as an additional set of features to get around this
2. Computation:
	- you have to compute the covariance matrix $\Sigma$, which may be too large to fit in memory (if you have thousands of features) or take too long to compute
	- secondly the eigenvalue decomposition is $O(n^3)$
3. Common ML "gotcha": calculate the scaling factors on the training data, and then you use equations (2) and (3) to apply the same scaling fctors to the test data, otherwise you are at risk of over-fitting (you would be using information from the test set in the training process)
## Density Estimaiton
- non-parametric: histogram, kernel density estimate
	- very flexible
	- little to no prior knowledge required
	- inference is easy
	- expensive in memory and CPU (must store all data)
	- not much opportunity to incorporate prior knowledge
- parametric: Gaussian mixture model
	- restricted family of functions
	- encode assumptions
	- compact representation
	- inflexible; model might be wrong
	- appropriate model might be obscure, complicated
- semi-parametric: Dirichlet process mixture model (infinite limit of GMM)
### Gaussian Mixture model
![[Screenshot 2025-02-09 at 12.12.10.png|500]]
### Kernel Density Estimation
![[Screenshot 2025-02-09 at 12.13.33.png|500]]