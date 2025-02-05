---
tags:
  - Lesson
  - multivariate_analysis
---
- samples consists of more than one variable
- descriptive statistics may be used to describe the relationship between pairs of variables
	- cross-tabulations and contingency tables
	- graphical representation via scatter-plots
	- quantitative measures of dependence
		- correlation (Pearson's r if both continuous else Spearman's rho)
		- covariance (reflects scale)
		- Mutual information
	- descriptions of conditional distributions
## Dimensionality reduction
- assume we are given a data set of (high-dimensional) input objects $\textbf{X} = \{x_i\}_{i=1,...,m,} \; x_i \in \mathcal{R}^n$ 
- aim is to learn a $k$-dimensional embedding in which each object is represented by a point $\textbf{P} = \{p_i\}_{i=1,...,m,} \; p_i \in \mathcal{R}^k$ 
- typical values for $k$ are 2. or 3 (for visualisation), in general $k << n$ 
## Linear dimensionality reduction
### Methods:
![[Principle Component Analysis (PCA)]]
![[Random Projections]]
## Nonlinear dimensionality reduction
![[Screenshot 2025-02-05 at 11.38.48.png|500]]
![[t-Distributed stochastic neighbour embedding]]