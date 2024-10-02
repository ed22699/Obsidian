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

![[Dual Representations]]
## Kernel functions are scalar products in feature space
- Suppose $\boldsymbol{x}$ is some test datapoint
- suppose, for example, we had 3 datapoints, $\boldsymbol{x}_1$, $\boldsymbol{x}_2$ and $\boldsymbol{x}_3$ and 2 features so
$$
\Phi\phi(\boldsymbol{x})=\begin{pmatrix}\phi_1(\boldsymbol{x}_1)&\phi_2(\boldsymbol{x}_1)\\\phi_1(\boldsymbol{x}_2)&\phi_2(\boldsymbol{x}_2)\\\phi_1(\boldsymbol{x}_3)&\phi_2(\boldsymbol{x}_3)\end{pmatrix}\begin{pmatrix}\phi_1(\boldsymbol{x})\\\phi_2(\boldsymbol{x})\end{pmatrix}=\begin{pmatrix}\phi(\boldsymbol{x}_1)^T\phi({x})\\\phi(\boldsymbol{x}_2)^T\phi({x})\\\phi(\boldsymbol{x}_3)^T\phi({x})\end{pmatrix}
$$
- if we define a kernel function: $k(\boldsymbol{x}, \boldsymbol{x}')=\phi(\boldsymbol{x})^T\phi(\boldsymbol{x}')$ then:
$$
\Phi\phi(\boldsymbol{x})=\begin{pmatrix}k(\boldsymbol{x}_1,\boldsymbol{x})\\k(\boldsymbol{x}_2,\boldsymbol{x})\\k(\boldsymbol{x}_3,\boldsymbol{x})\end{pmatrix}
$$
![[The kernel trick]]
## Similarity
- kernel function represents the degree of similarity between its two arguments
	- kernel functions are **always symmetric**
- high kernel value represents a high degree of similarity
with our example
$$
y(\boldsymbol{x})=\boldsymbol{a}^T\begin{pmatrix}k(\boldsymbol{x}_1,\boldsymbol{x})\\k(\boldsymbol{x}_2,\boldsymbol{x})\\k(\boldsymbol{x}_3,\boldsymbol{x})\end{pmatrix}=a_1k(\boldsymbol{x}_1,\boldsymbol{x})+a_2k(\boldsymbol{x}_2,\boldsymbol{x})+a_3k(\boldsymbol{x}_3,\boldsymbol{x})
$$
- prediction for $\boldsymbol{x}$ is a linear function of the similarities between $\boldsymbol{x}$ and each element of the training data
- unlike linear regression it looks like we have to keep the entire training set around to make predictions but in fact we only need those $\boldsymbol{x}_i$ where $a_i \neq 0$ 
## Learning with kernels
- so far we've made predictions using a learned value of the dual parameter vector $\boldsymbol{a}$
- if we needed to compute feature values $\phi(\boldsymbol{x})$ to learn $\boldsymbol{a}$, then the advantage of using kernels would disappear
- however, for many models we can learn $\boldsymbol{a}$ just using kernels
- learning and prediction just require evaluating kernel functions
### The Gram Matrix
- gram matrix $\boldsymbol{K}$ is defined to be $\Phi\Phi^T$ 
- $K_{nm}=\phi(\boldsymbol{x}_n)^T\phi(\boldsymbol{x}_m)=k(\boldsymbol{x}_n, \boldsymbol{x}_m)$ is the similarity between the $n^{th}$ and $m^{th}$ datapoint
	- given data $\boldsymbol{x}_n$ and a particular choice of kernel $k$, we can computer the Gram matrix $\boldsymbol{K}$
	




slack variable