---
tags:
  - Lesson
  - Regression_and_Discriminant
---
# Regression
Finding a relationship between two variables
## Deterministic model
- **Data**: a set of data points $D = \{(x_{1}, y_{1}), (x_{2}, y_{2}), ..., (x_{N}, y_{N})\}$ where $x_{i}$ is the number of rooms in house $i$ and $y_{i}$ the house value
- **Task**: build a model that can predict the house value from the number of rooms
- **Model Type**: [[Parametric]]; assumes polynomial relationship between house value and number of rooms
- **Model Complexity**: assume linear relationship $y_{i} = a_{0} + a_{1}x_{i}$
### Fitting
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
### Linear regression for nonlinear models
- for a polynomial of degree $p+1$ we use:
$$
y_{i} = a_{0} + a_{1}x_{i}+a_{2}x_{i}^{2}+...+a_{p}x_{i}^{P}
$$
	- note $p > 1$ give a nonlinear regression