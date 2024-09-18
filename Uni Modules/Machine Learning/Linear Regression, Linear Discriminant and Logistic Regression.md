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
 ![[Fitting]]
### Linear regression for nonlinear models
- for a polynomial of degree $p+1$ we use:
$$
y_{i} = a_{0} + a_{1}x_{i}+a_{2}x_{i}^{2}+...+a_{p}x_{i}^{P}
$$
- note $p > 1$ give a nonlinear regression
- to model this as a linear regression we would need [[Fitting]]
## Regression with probabilistic models
- core part of ML:
	- capture uncertainty the model has about data
- let $\epsilon$ capture the uncertainty
	- house price $=$ $a_{1}$ $\times$ number of rooms $+$ $\epsilon$ 
- assume $\epsilon$ is given by 
