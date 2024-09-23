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
- assume $\epsilon$ is given by $N(\mu  = 0, \sigma^{2})$ which gives the likelihood
$$
p(y|X,\theta) = \Pi_{i=1}^{N}p(price_{i}|rooms_{i},\theta)= \Pi_{i=1}^{N}\frac{1}{\sqrt{2\pi}\sigma}e^{-\frac{1}{2}\frac{(price_{i}-a_{1}rooms_{i})^{2}}{\sigma^{2}}}
$$
![[Screenshot 2024-09-18 at 15.54.32.png|300]]
![[Maximum Likelihood Estimation]]
# Deterministic vs Probabilistic
- Probabilistic models (e.g. [[Maximum Likelihood Estimation]]) can tell us more
- we could use the same MLE recipe to find $\sigma_{ML}$. This would show how uncertain our model is about the data $D$ 
- e.g. for datasets $D_{1}$ and $D_{2}$ the parameters $\theta = \{a_{1}, \sigma\}$ would be 
![[Screenshot 2024-09-18 at 16.21.14.png|600]]
# Classification
- an example of [[Supervised Learning]]
- Goal: Classify input data into one of K classes
- Model: Discriminant function (function that takes an input vector $x$ and assigns it to class $C_{k}$)
	- is $K = 2$ then it is a linear function
 ![[Linear Discriminant Function]]
![[Logistic Regression]]
	

# Reading
- Bishop 3.1 up to end of 3.1.1.
- Bishop 4 up to end of 4.1.1.
- Bishop 4.3.2.