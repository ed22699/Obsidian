---
tags:
  - Article
---
- most difficult optimisation problem is neural network training
- chapter focuses on one case: finding the parameters $\theta$ of a neural network that significantly reduce a cost function $J(\theta)$
## How Learning Differs from Pure Optimisation
- machine learning usually acts indirectly
	- we care about some performance measure $P$, that is defined with respect to the test set and may also be intractable
	- therefore optimise $P$ only indirectly
	- we reduce a different cost function $J(\theta)$ in hope to improve $P$
- typically the cost function can be written as an average over the training set
$$
J(\theta) = \mathbb E _{(x,y)\sim \hat p_{data}}L(f(x;\theta),y)
$$
- where
	- $L$ is the per-example loss function
	- $f(x;\theta)$ is the predicted output when the input is $x$
	- $\hat p _{data}$ is the empirical distribution 
- we would usually prefer to minimise the corresponding objective function where the expectation is taken across the data generating distribution rather than just over the finite training set
$$
J^*(\theta) = \mathbb E _{(x,y)\sim \hat p_{data}}L(f(x;\theta),y)
$$
### Empirical Risk Minimisation
- goal is to reduce expected generalisation error given by the equation
	- this quantity is known as the *risk*
- the expectation is taken over the true underlying distribution $p_{data}$
	- if we knew the true distribution $p_{data}(x,y)$ risk minimisation would be an optimisation task solvable by an optimisation algorithm
	- we don't know $p_{data}(x,y)$, only have training set of samples
- is a machine learning problem
	- convert ML problem to optimisation problem by minimising the expected loss on the training set (replace true distribution with empirical distribution defined by the training set)
	- minimise the *empirical risk*
	$$
	\mathbb E_{x,y \sim \hat p_{data}(x,y)}[L(f(x;\theta),y)] = \frac 1 m \sum _{i=1}^m L(f(x^{(i)}; \theta), y^{(i)})
	$$
	- where $m$ is the number of training examples
- training process based on minimising this average training error is known as *empirical risk minimisation* 
	- prone to overfitting
	- not really feasible
- most effective modern optimisation algorithms are based on gradient descent
### Surrogate Loss Functions and Early Stopping
- sometime loss function we care about is not one that can be optimised efficiently 
	- typically optimise a *surrogate loss function* instead
		- acts as a proxy
- a machine learning algorithm usually minimises a surrogate loss function but halts when a convergence criterion based on early stopping is satisfied
	- early stopping criterion is based on true underlying loss function measured on a validation set
### Batch and Minibatch Algorithms
- the objective function usually decomposes as a sum over the training examples
- optimisation algorithms for machine learning typically compute each update to the parameters based on an expected value of the cost function estimated using only a subset of the terms of the full cost function
	- computing this expectation exactly is very expensive, in practice we compute these expectations by randomly sampling a small number of examples from the dataset, then taking the average
	- rapidly computing approximate estimates of the gradient rather than exact causes a faster convergence 
- optimisation algorithms that use the entire training set are called *batch* or *deterministic* gradient methods
	- process all the training examples simultaneously in a large batch
	- don't get confused by batch size which often describes the size of a minibatch
- optimisation algorithms that use only a single example at a time are sometimes called *stochastic* and sometimes *online* methods
	- the term online is usually reserved for when the examples are drawn from a stream of continually created examples rather than fixed-size training set
- most algorithms for deep learning fall somewhere in between, use more than one but fewer than all the training examples
	- traditionally called *minibatch* or *minibatch stochastic* methods, now common to call them simply *stochastic* methods

276