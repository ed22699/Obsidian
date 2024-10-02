---
tags:
  - kernal_support_vector
---
- kernel-based method for classification which avoids the excessive computation
consider a simple linear model for two class classification:
$$
y(\boldsymbol{x})=\boldsymbol{w}^T\phi(\boldsymbol{x})+b
$$
- bias $b$ has been made explicit 
- class label is either $-1$ or $1$

- assume (optimistically) the training dataset is linearly separable
	- some $\boldsymbol{w}$ and $b$ s.t. $y(\boldsymbol{x}_n)>0$ if $t_n = 1$ and $y(\boldsymbol{x}_n)< 0$ if $t_n=-1$ 
		- $t_ny(\boldsymbol{x}) > 0$ $\forall$ $\boldsymbol{x}_n$

>[!note]	
typically more than one hyperplane that separates classes

### Maximum margin classifiers
- natural choice is the hyperplane which maximises the margin (distance from the hyperplane to the closest training datapoint)
- the training data points closest to the separating hyperplane are the support vectors, in a sense they are the training datapoints 'that matter'
![[Screenshot 2024-10-02 at 16.32.05.png|300]]
- the learning problem we have to solve is:
