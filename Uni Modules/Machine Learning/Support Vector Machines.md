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
	- subject to the linear inequality constraints (2)
	- quadratic programming problem 
#### Dual representation
[[Dual Representations]] of the maximum margin problem is to maximise: 
$$
\tilde{L}(\boldsymbol{a})= \sum_{n=1}^Na_n-\frac 12\sum_{n=1}^N\sum_{m=1}^Na_na_mt_nt_mk(\boldsymbol{x_n, \boldsymbol{x}_m})
$$
- with constraints
	- $a_n \geq 0, \quad n=1,...,N$ 
	- $\sum_{n=1}^Na_nt_n=0$
- $k(\boldsymbol{x}_n, \boldsymbol{x}_m)=\phi(\boldsymbol{x}_n)^T\phi(\boldsymbol{x}_m)$
- another quadratic problem
- this can be derived from the original one by using Lagrange multipliers ($a_n$)

#### SVM
- to learn a max margin classifier we need the $k(\boldsymbol{x}_n, \boldsymbol{x}_m)$ values ([[Gram Matrix]])
	- do not need to compute $\phi(\boldsymbol{x}_n)$ so $\phi(\boldsymbol{x}_n)$ can be as high-dimensional as we like
- to classify a new datapoint we compute $y(\boldsymbol{x})=\sum_{n=1}^Na_nt_nk(\boldsymbol{x}, \boldsymbol{x}_n)+b$
	- again only the kernel function is needed
	- typically for most training datapoints $\boldsymbol{x}_n$ we have $a_n=0$ (not needed for making predictions)
	- needed points are called **support vectors**
## SVM kernels
>[!todo]
Look at Jupyter notebook example

- default kernel for NuSVC is the RBF kernel: $k(\boldsymbol{x}, \boldsymbol{x}')=e^{-\gamma||\boldsymbol{x}-\boldsymbol{x}'||^2}$
	- implicit feature space is infinite dimensional
	- is non-parametric (number of support vectors, and thus dual parameters, depends on the data and value of $\gamma$)
		- $\gamma$ defines how far the influence of a single training example reaches
			- low values mean far
			- high values mean close
			- can be seen as inverse of the radius of influence of samples selected by the model as support vectors
- data does not need to be real numbers, can also be: graphs, text documents, images, websites, etc.
	- for any sort of $\boldsymbol{x}$ as long as we have a kernel function $k(\boldsymbol{x}, \boldsymbol{x}')$, measuring the similarity between $\boldsymbol{x}$ and $\boldsymbol{x}'$ we can apply kernel-based machine learning such as SVMs
>[!todo]
see paper on slide 21

- RBF is a popular choice of kernel
- you can construct a new kernel function from existing known kernels, however, the function you define must be symmetric and any Gram matrix $\boldsymbol{K}$ must be a positive semidefinite matrix
## Soft margins
if you want a wide margin then you might have to allow training points to be inside the margin, or even on the wrong side of the decision boundary
![[Drawing 2024-10-04 09.15.33.excalidraw|200]]
- earlier we had the following problem: $\min_{w,b}\frac12w^Tw$
	- subject to $t_n(w^T\phi(x_n)+b)\geq 1$ 
- scikit learn actually solves the following optimisation: $\min_{w,b,\varepsilon}\frac 1 2 w^Tw+C\sum_{n=1}^N\varepsilon_n$ 
	- subject to $t_n(w^T\phi(x_n)+b)\geq1-\varepsilon_n, \quad \varepsilon_n\geq0,n=1,...,N$
	- points for which $0<\varepsilon\leq1$ lie inside the margin but on the correct side of the boundary
	- points which $\varepsilon_n>1$ lie on the wrong side of the decision boundary and are misclassified
- this is a soft margin
	- being on the wrong side of the margin is merely penalised 
	- $C$ is a regularisation parameter 
>[!todo]
see slide 27

![[Screenshot 2024-10-04 at 09.32.14.png|300]]
- plots above are defined by $\sum_{i\in SV}y_i\alpha_iK(x_i,x)+b$ 
## Multi-class classification
- SVMs are fundamentally two class classifiers
- if there are $k$ classes use:
	- one-versus-one: where we train $\frac{k(k-1)}{2}$ SVM classifiers to distinguish between each pair of classes and then take a vote for the predicted class
	- one-versus-the-rest: where we train $k$ SVM classifiers to distinguish between each class and all other classes
- in scikit-learn, SVC and NuSVC go for one-versus-one and LinearSVC does one-versus-the-rest
>[!todo]
see page 31

