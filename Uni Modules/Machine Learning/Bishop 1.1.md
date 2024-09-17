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
