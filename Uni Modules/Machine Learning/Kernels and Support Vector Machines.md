---
tags:
  - Lesson
  - kernal_support_vector
---
## tldr version
suppose we're doing classification where each training data point is $(x,y)$
**Standard approach**:
- choose a function $\phi$, map each raw data vector $\boldsymbol{x}$ into a feature vector $\phi (\boldsymbol{x})$ 
- learn parameters using the feature vectors and class labels
	- when making a predictor for a test data vector $\boldsymbol{x}'$ first encode as $\phi(\boldsymbol{x}')$ and use learned model to make prediction
**Kernel approach**:
- choose a kernel function $k$ which measures similarity between raw data vectors $k(\boldsymbol{x}_m, \boldsymbol{x}_n)$ 
- learn parameters using the $k(\boldsymbol{x}_m, \boldsymbol{x}_n)$ values and class labels
	- when making a prediction for a test data vector $\boldsymbol{x}'$ use learned parameters and values of $k(\boldsymbol{x}_n, \boldsymbol{x}')$ to make a prediction

[[Linear Regression, Linear Discriminant and Logistic Regression]]
![[The kernel trick]]