---
tags:
  - kernal_support_vector
---

- let $N$ be the size of the data
- let $\Phi$ be the design matrix whose $n^{th}$ row is just the feature vector for the $n^{th}$ datapoint
we can write the minimising value of $\boldsymbol{w}$ in terms of an N-dimensional parameter vector $\boldsymbol{a}$ as $\boldsymbol{w}=\Phi^T \boldsymbol{a}$, so that:
$$y(\boldsymbol{x})=\boldsymbol{w}^T\phi(\boldsymbol{x})=\boldsymbol{a}^T \Phi \phi(\boldsymbol{x})$$
- dual parameters $a_n$ are the ($\lambda$-adjusted) residuals: $a_n=-\frac 1 \lambda (\boldsymbol{w}^T\phi(\boldsymbol{x}_n)-t_n)$ 
- replaced an M-dimensional parameter vector with an N-dimensional one
	- to make a prediction for a new datapoint we have to use the entire training set (i.e. $\Phi$)
	- seems like a bad idea
using $\boldsymbol{a}$ is known as a dual representation