---
tags:
  - statistics_excel
---
- able to simultaneously analyse the impact of several independent variables on a dependent variable
- goal is to describe the impact of a set of independent variables $X_j$ on a dependent variable $Y$ and to determine what happens to $Y$ when a variable $X_j$ is changed
- using the ordinary least squares method, we minimise the squared deviations of the regression function from the observed $y_i$-values
$$
\sum e_i ^2 = \sum (y_i - (b_0 + b_1 x_{1i} + b_2x_{2i}+...+b_jx_{ji}))^2 \rightarrow min!
$$
- we obtain the regression function with the estimated coefficients
$$
\hat Y = b_0 +b_1X_1 + b_2X_2 + ... + b_JX_J
$$
- where
	- $b_0$ is the intercept
	- $b_1 \; to \; b_J$ are the estimated coefficients for the independent variables $X_j$
	- $J$ is the number of independent variables
	- $\hat Y$ are the estimated values using the regression function