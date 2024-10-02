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
$$
\arg \max_{w,b}\{\frac {1}{||w||}\min_n[t_n(\boldsymbol{w}^T\phi(\boldsymbol{x}_n)+b)]\}
\tag{1}
$$
- we can rescale $\boldsymbol{w}$ and $b$ so that for a point $\boldsymbol{x}_n$ that is closest to the separating hyperplane $t_n(\boldsymbol{w}^T\phi(\boldsymbol{x}_n)+b)=1$ 
- and for all datapoints: 
$$ t_n(\boldsymbol{w}^T\phi(\boldsymbol{x}_n)+b)\geq 1 \qquad n=1,...,N \tag{2}$$  
- plugging back into (1) we now just need to maximise $\frac{1}{||\boldsymbol{w}||}$ which is the same as minimising: $\arg\min_{\boldsymbol{w},b}\frac 1 2 ||\boldsymbol{w}||^2$
	- subject to the li ear inequality constraints (2)
	- quadratic programming problem 