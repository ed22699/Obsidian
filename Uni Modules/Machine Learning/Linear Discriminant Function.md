---
tags:
  - Regression_and_Discriminant
---

- simplest LD is $y(x) = w_{0}+\boldsymbol{w}^{\boldsymbol{T}}\boldsymbol{x}$ 
	- $y$ is used to predict class $C_{k}$, $x$ is the input vector (feature values)
	- $w_{0}$ is a scalar (called bias)
	- $\boldsymbol{w}_{\boldsymbol{T}}$ is our vector of parameters (called weights)
- for $K = 2$: an input vector $x$ is assigned to class $C_{1}$ if $y(x) \geq 0$ and to class $C_{2}$ otherwise
> [!note] 
> Direct application of least-squares to choose $w_{0}$ and $\boldsymbol{w}$ does not give great results

- instead assume data from each class has a Gaussian distribution whose mean is class-specific (but where the covariance matrix for each class is the same), use [[Maximum Likelihood Estimation]] to find parameters for each of these Gaussians and finally use [[Bayes theorem]] to assign classes 
## LD and linear separability
- when two sets of points are separable by a line
![[Screenshot 2024-09-18 at 16.40.03.png|500]]