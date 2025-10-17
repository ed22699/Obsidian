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
- canonical example of a stochastic method is stochastic gradient descent
	- minibatch sizes are generally driven by the following factors:
		- larger batches provide a more accurate estimate of the gradient, but with less that linear returns
		- multicore architectures are usually underutilised by extremely small batches
			- motives using some absolute minimum batch size, below which there is no reduction in the time to process a minibatch
		- if all examples in the batch are to be processed in parallel, then the amount of memory scales with the batch size 
			- many hardware setups this is the limiting factor
		- some kinds of hardware achieve better runtime with specific sizes of arrays (especially when using GPUs)
			- common for power of 2 batch sizes to offer better runtime
			- typical power of 2 batch sizes range from 32 to 256, with 16 sometimes being attempted for large models
		- small batches can offer a regularising effect perhaps due to the noise they add to the learning process
			- generalisation error is often best for a batch size of 1
			- may require a small learning rate to maintain stability because of the high variance in the estimate of the gradient
			- total runtime can be very high as a result of the need to make more steps, both because of the reduced learning rate and because it takes more steps to observe the entire training set
- different kinds of algorithms use different kinds of information from the minibatch
	- some more sensitive to sampling error
	- methods that compute updates based only on the gradient $g$ are usually relatively robust and can handle smaller batch sizes, like 100
	- second-order methods, which also use the Hessian matrix $H$ and compute updates such as $H^{-1}g$ typically require much larger batch sizes, like 10,000
		- required to minimise fluctuations in the estimates of $H^{-1}g$
- crucial minibatches be selected randomly
	- computing an unbiased estimate of the expected gradient requires samples to be independent
	- we also wish for two subsequent gradient estimates to be independent from each other
		- reduces bias
		- can be computationally expensive to shuffle a very large batch
			- in practice it is usually sufficient to shuffle the order of the dataset once and then store it in a shuffled fashion
				- does not seem to have a significant detrimental effect
- motivation for minibatch stochastic gradient descent is that it follows the gradient of the true *generalisation error* as long as no examples are repeated
	- on a second pass the estimate becomes biased because it is formed by resampling values that have already been used
	- easiest to see in online learning where minibatches are drawn from a stream of data
- equivalence is easiest to derive when both $x$ and $y$ are discrete, here the generalisation error can be written as a sum
$$
J^*(\theta)=\sum_x \sum_y p_{data}(x,y)L(f(x;\theta),y)
$$
- with the exact gradient 
$$
g = \nabla _\theta J^* (\theta) = \sum_x \sum_y p_{data}(x,y)\nabla_\theta L(f(x;\theta), y)
$$
- similar result can be derived when $x$ and $y$ are continuous under mild assumptions regarding $p_{data}$ and $L$
	- can obtain an unbiased estimator of the exact gradient of the generalisation error by sampling a minibatch of examples $\{x^{(1)}, ..., x^{(m)}\}$ with corresponding targets $y^{(i)}$ for the data-generating distribution $p_{data}$, then computing the gradient of the loss with respect to the parameters for that minibatch
$$
\hat g = \frac 1 m \nabla _\theta \sum_i L(f(x^{(i)}; \theta), y^{(i)})
$$
- updating $\theta$ in the direction of $\hat g$ performs SGD on the generalisation error
	- interpretation only applies when examples are not reused
	- however it is usually best to make several passes through the training set, unless the training set is extremely large
		- the additional epochs usually provide enough benefit due to decreased training error to offset the harm they cause by increasing the gap between training error and test error
- it is becoming more common for machine learning applications to use each training example only once or even to make an incomplete pass through the training set
	- for an extremely large training set overfitting is not an issue, so underfitting and computational efficiency become the predominant concerns
## Challenges in Neural Network Optimisation
- when training neural networks, we must confront the general non-convex case
### Ill-Conditioning
- most prominent issue is ill-conditioning of the Hessian matrix $H$
- can manifest by causing SGD to get stuck so even very small steps increase the cost function
- recall equation for second-order Talor series expansion of the cost function predicts that a gradient descent step of $-\epsilon g$ will add to the cost
$$
\frac 1 2 \epsilon ^2 g^T Hg-\epsilon g^T g
$$
- gradient become a problem when $\frac 1 2 \epsilon ^2 g^THg$ exceeds $\epsilon g^Tg$ 
- to determine whether ill-conditioning is detrimental to a neural network training task, monitor the squared gradient norm $g^Tg$ and the $g^THg$ term
	- many cases, gradient norm does not shrink significantly but the $g^THg$ term grows by more than an order of magnitude
	- learning becomes very slow despite the presence of a strong gradient because the learning rate must be shrunk to compensate for even stronger curvature
### Local Minima

281