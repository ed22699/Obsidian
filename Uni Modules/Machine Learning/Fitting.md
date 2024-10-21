---
tags:
  - Regression_and_Discriminant
---

- modelling non-linear data linearly 
1. Find $\theta = (a_{0}, a_{1})$ which minimises the <u>sum of squared residuals</u>:
$$
R(a_{0}, a_{1}) = \sum_{i=1}^{N}(y_{i} - (a_{0}+a_{1}x_{i}))^{2}
$$
2. Using matrix notation we have:
	$$
	\frac{dR}{d\theta} = -2X^{T}(y-X\theta)
	$$
	- $X_{ij}$ is the value of the $j$th feature in the $i$th datapoint (we also add a fake feature which is always 1 to handle the intercept)
	- $y_{i}$ is the value of the response in the $i$th datapoint
3. Set $\frac{dR}{d\theta}$ to $0$ and re-arrange:
$$
\hat{\theta} = (X^{T}X)^{-1}X^{T}y
$$
#### Example

| x   | -1  | 0   | 1   | 2   |
| --- | --- | --- | --- | --- |
| y   | 0   | 1   | 3   | 9   |
$y = \begin{pmatrix} 0 \\ 1 \\ 3 \\ 9 \end{pmatrix}$ $X = \begin{pmatrix}1 & -1 \\ 1 & 0 \\ 1 & 1 \\ 1 & 2 \end{pmatrix}$  
$X^{T}X = \begin{pmatrix}1 & 1& 1&1\\-1&0&1&2 \end{pmatrix}\begin{pmatrix}1 & -1 \\ 1 & 0 \\ 1 & 1 \\ 1 & 2 \end{pmatrix} = \begin{pmatrix}4&2\\2&6 \end{pmatrix}$ 
$\hat{\theta} = (X^{T}X)^{-1}X^{T}y = \frac{1}{20}\begin{pmatrix}6&-2\\-2&4 \end{pmatrix}\begin{pmatrix}1&1&1&1\\-1&0&1&2 \end{pmatrix} \begin{pmatrix}0\\1\\3\\9 \end{pmatrix} = \begin{pmatrix}1.8\\2.9 \end{pmatrix}$ 
$y = 1.8 + 2.9x$ 