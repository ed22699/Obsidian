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
## Regularised Linear Regression
[[Linear Regression, Linear Discriminant and Logistic Regression]]
Suppose we are doing regularised linear regression by minimising regularised sum of squared error:
$$
J(\boldsymbol{w})=\frac 1 2 \sum_{n=1}^N(\boldsymbol{w}^T\phi(\boldsymbol{x})-t_n)^2+\frac \lambda 2 \boldsymbol{w}^T \boldsymbol{w}
$$
- $\boldsymbol{w}$ is the M-dimensional parameter vector to be learned from the data (includes a component for the intercept)
- $\boldsymbol{x}$ is some datapoint
- $\phi(\boldsymbol{x})$ is the M-dimensional feature vector which $\boldsymbol{x}$ gets mapped to by the basis functions
- $\frac \lambda 2 \boldsymbol{w}^T \boldsymbol{w}$ is the regularisation term which pushes parameters which are not helping much to fit the data towards zero
## Dual Representations
- let $N$ be the size of the data
- let $\Phi$ be the design matrix whose $n^{th}$ row is just the feature vector for the $n^{th}$ datapoint
we can write the minimising value of $\boldsymbol{w}$ in terms of an N-dimensional parameter vector $\boldsymbol{a}$ as $\boldsymbol{w}=\Phi^T \boldsymbol{a}$, so that:
- $y(\boldsymbol{x})=\boldsymbol{w}^T\phi(\boldsymbol{x})=\boldsymbol{a}^T \Phi \phi(\boldsymbol{x})$
- so dual parameters $a_n$ are the ($\lambda$-adjusted) residuals: $a_n=-\frac 1 \lambda (\boldsymbol{w}^T\phi(\boldsymbol{x}_n)-t_n)$ 
	- replaced an M-dimensional parameter vector with an N-dimensi
- using $\boldsymbol{a}$ is known as a dual representation






![[The kernel trick]]
slack variable