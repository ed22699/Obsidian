---
tags:
  - MLConcepts
---
# Feature Extraction
- pre-processing to ensure easier situations for the model
	- in digit recognition the images of the digits are typically translated and scaled so that each digit is contained within a box of a fixed size - reduces variability within each digit class (location and scale are now equal)
- pre-processing can speed up computation through dimensionality reduction (less features than pixels so less dimensions compared to no preprocessing)
	- facial recognition aim to find features that are fast to compute, yet preserve useful discriminatory information
- features used as inputs to the pattern recognition algorithm

## Supervised learning
- classification problems - aim is to assign each input vector to one of a finite number of discrete categories 
- regression - desired output consists of one or more continuous variables
## Unsupervised learning
- clustering - discover groups of similar examples within the data
- density estimation - determine the distribution of data within the input space
- visualisation - project the data from a high-dimensional space down to two or three dimensions 
# Polynomial Curve Fitting
- regression problem
## Example
- suppose we observe a real-valued input variable $x$ and we with to use this observation to predict the value of a real-valued target variable $t$
- data is generated from the function $\sin(2\pi x)$ with random noise included in the target values
- suppose training set comprising of $N$ observations of $x$, written $\bar{x} \equiv (x_{1}, ..., x_{N})^{T}$, together with corresponding observations of the values of $t$, denoted $\bar{t} \equiv (t_{1},...,t_{N})^{T}$  
### Aim
- exploit training set in order to make predictions of the value $\hat{t}$ of the target variable for some new value $\hat{x}$ 
### Method
- involves implicitly trying to discover the underlying function $\sin(2\pi x)$ 
- difficult as:
	- finite data set
	- noise
Consider curve fitting, in particular the polynomial form
$$
y(x,\bar{w}) = w_{0} + w_{1}x + w_{2}x^{2}+...+w_{M}x^{M} = \sum_{j=0}^{M}w_{j}x^{j}
$$
where $M$ is the order of the polynomial and $x^{j}$ denotes $x$ raised to the power of $j$. $w_{0},...,w_{M}$ are collectively denoted by the vector $\bar{w}$
- although polynomial function $y(x, \hat{w})$ is nonlinear function of $x$,it is a linear function of the coefficients $\bar{w}$ 
- values of coefficients are determined by fitting the polynomial to the training data. Done by minimising the error function between the function $y(x, \bar{w})$ for any given value of $\bar{w}$ 
	- one error function is the sum of squares which aims to minimise the distance between the prediction $y(x_{n}, \bar{w})$ and the point $x_{n}$ and its corresponding target value $t_{n}$
	$$
	E(\bar{w}) = \frac{1}{2} \sum_{n=1}^{N}\{y(x_{n}, \bar{w}) - t_{n}\}^{2}
	$$
	![[Screenshot 2024-09-17 at 12.58.45.png|200]]
- We solve curve fitting problem by choosing the value of $\bar{w}$ for which $E(\bar{w})$ is as small as possible
p6