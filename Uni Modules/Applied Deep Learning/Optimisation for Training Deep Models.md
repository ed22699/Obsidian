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
- one of the most prominent features of a convex optimisation problem is that it can be reduced to a problem of finding a local minimum
	- any local minimum is guaranteed to be a global minimum  
- non-convex functions will likely have many local minima
- neural networks have multiple local minima because of the *model identifiability* problem
	- model is identifiable if a sufficiently large training set can rule out all but one setting of the model's parameters
	- models with latent variables are often not identifiable
	- if we have $m$ layers with $n$ units each, then there are $n!^m$ ways of arranging the hidden units. This kind of non-identifiability is known as *weight space symmetry*
	- additional causes for non-identifiability in neural network
- identifiability issues mean neural network cost function can have an extremely large amount of local minima
	- however, all local minima arising from non-identifiability are equivalent to each other in cost function value
		- these local minima are not a problematic form of nonconvexity
- local minima problematic if high cost in comparison to the global minimum
	- if common could pose issue for gradient-based optimisation algorithms
	- experts now suspect, for a sufficiently large neural network, most local minima have a low cost function value and that it is not important to find a true global minimum rather than to find a point in parameter space that has low but not minimal cost
- a test that can rule out local minima as the problem is *plotting the norm of the gradient over time*
	- if norm of gradient does not shrink to insignificant size, problem is neither local minima nor any other kind of critical point
	- can be difficult to positively establish local minima are a problem in high-dimensional spaces
		- many structures other than local minima also have small gradients
### Plateaus, Saddle Points and Other Flat Regions
- saddle point is a point with zero gradient
- at the saddle point the Hessian matrix has both positive and negative eigenvalues
- can think of a saddle point as being a local minimum along one cross-section of the cost function and a local maximum along another cross-section
- saddle point are more common than local minima in higher-dimensional spaces
- for a function $f:\mathbb R^n \rightarrow \mathbb R$ of this type, the expected raton of the number of saddle points to local minima grows exponentially with $n$
	- think of it as in a higher dimension you are flipping more coins, it is less likely all will be heads
- local minima are ch more likely to have low cost than high cost in a higher-dimensional space 
	- critical points with high cost are more likely saddle points
	- extremely high cost more likely local maxima
- gradient descent seems able to escape saddle points in many cases 
- saddle points are a problem for Newton's method as it tries to solve for a point where the gradient is zero
	- saddle-free Newton method for second-order optimisation showed significant improvements over the traditional version
		- holds promise if it can be scaled
- maxima are much like saddle points from the perspective of optimisation
	- many algorithms are not attracted to them, but unmodified Newton's method is
### Cliffs and Exploding Gradients 
- neural networks with many layers often have extremely steep regions resembling cliffs
	- result from the multiplication of several large weights together
	- on the face of cliff, gradient update step can move the parameters extremely far
- its most serious consequences can be avoided using the *gradient clipping* heuristic
	- recall that the gradient specifies not the optimal step size, but only the optimal direction within an infinitesimal region
	- when gradient descent algorithm proposes a very large step, gradient clipping heuristic intervenes to reduce the step size, making it less likely to go outside the region where the gradient indicates the direction of approximately steepest descent
- cliffs most common in the cost functions for recurrent neural networks
	- as such models involve a multiplication of many factors, with one factor for each time step
	- long temporal sequences thus incur an extreme amount of multiplication
### Long-Term Dependencies
- issue when computation graph becomes extremely deep
	- e.g. recurrent networks
	- repeated application of the same parameters gives rise to especially pronounced difficulties
- *vanishing and exploding gradient problem* refers to the fact that gradients through such a graph are also scaled according to $diag(\lambda)^t$ 
	- vanishing gradients make it difficult to know which direction the parameters should move to improve the cost function
	- exploding gradients can make learning unstable
		- such as the cliff structures
### Inexact Gradients 
- most optimisation algorithms designed with assumption that we have access to the exact gradient or Hessian matrix
	- usually have only a noisy or even biased estimate of there quantities
	- most rely on sampling-based estimates
- can avoid by choosing a surrogate loss function that is easier to approximate than the true loss
### Poor Correspondence between Local and Global Structure
### Theoretical Limits of Optimisation 
- there are limits on the performance of any optimisation algorithm we might design for neural networks
## Basic Algorithms
### Stochastic Gradient Descent (SGD)
- probably the most used in general particularly for deep learning
- crucial parameter is the learning rate
	- in practice, it is necessary to gradually decrease the learning rate over time, so we now denote the learning rate at iteration $k$ and $\epsilon _k$ 
		- because gradient estimator introduces a source of noise (the random sampling of $m$ training examples) that does not vanish even when we arrive at a minimum
	- batch gradient descent can use a fixed learning rate as total cost function becomes 0 when we approach and reach a minimum
![[Screenshot 2025-10-20 at 00.17.45.png|400]]
- a sufficient condition to guarantee convergence of SGD is that 
$$
\sum _{k=1} ^\infty \epsilon_k = \infty
$$
and 
$$
\sum_{k=1}^\infty \epsilon_k^2 < \infty
$$
- in practice, it is common to decay the learning rate linearly until iteration $\tau$: $\epsilon _k = (1-\alpha)\epsilon _0 + \alpha \epsilon _\tau$
	- with $\alpha = \frac k \tau$, after iteration $\tau$, it is common to leave $\epsilon$ constant
- learning rate may be chosen by trail and error
	- best to choose by monitoring learning curves that plot the objective function as a function of time
- usually $\tau$ may be set to the number of iterations required to make a few hundred passes through the training set
- usually $\epsilon_\tau$ should be set to roughly 1 percent of the value of $\epsilon _0$
	- if $\epsilon _0$ is too large learning curve will show violent oscillations, with cost function often increasing significantly
- if learning rate is too low, learning proceeds slowly, may become stuck with a high cost value
- optimal initial learning rate, in terms of total training time and the final cost value is higher than the learning rate that yields the best performance after the first 100 iterations or so
	- best to monitor the first several iterations and use a learning rate that is higher than the best-performing learning rate at this time, but not so high that it causes severe instability
- to study convergence rate of an optimisation algorithm common to measure the excess error $J(\theta) - \min_\theta J(\theta)$ 
### Momentum
- designed to accelerate learning, especially in the face of high curvature, small but constant gradients, or noisy gradients
- introduces a variable $v$ that plays the role of velocity
	- the direction and speed at which the parameters move through parameter space
	- set to an exponentially decaying average of the negative gradient
$$
v \leftarrow \alpha v - \epsilon \nabla _\theta (\frac 1 m \sum_{i=1}^mL(f(x^{(i)};\theta), y^{(i)}))
$$
$$
\theta \leftarrow \theta + v
$$
![[Screenshot 2025-10-20 at 23.51.35.png|500]]
- the more previous gradients affect the current direction
- the size of the step depends on how large and how aligned a sequence of gradients are
	- largest when successive gradients point in exactly the same direction
	- if the momentum algorithm always observes gradient $g$, then it will accelerate in the direction of $-g$ until reaching a terminal velocity where the size of each step is $\frac{\epsilon ||g||}{1-\alpha}$
- common values of $\alpha$ include 0.5, 0.9, and 0.99
	- $\alpha$ may also be adapted over time, typically begins with a small value and is later raised
	- adapting $\alpha$ over time is less important than shrinking $\epsilon$ over time
- position of particle given by $\theta(t)$
- particle experiences net force $f(t)$, this force causes the particle to accelerate
$$
f(t)=\frac{d^2}{dt^2}\theta(t)
$$
- we can introduce the variable $v(t)$ representing the velocity of the particle at time $t$
$$
v(t) = \frac d {dt}\theta(t)
$$
$$
f(t)= \frac d{dt}v(t)
$$
- we add viscous drag to make sure it doesn't go back and forth forever
	- proportional to $-v(t)$
	- causes particle to gradually lose energy over time, eventually converging
### Nesterov Momentum
- variant of momentum inspired by Nesterov's accelerated gradient method
$$
v \leftarrow \alpha v - \epsilon \nabla _\theta [\frac 1 m \sum_{i=1}^n L(f(x^{(i)}; \theta +\alpha v), y^{(i)})]
$$
$$
\theta \leftarrow \theta +v
$$
- with this gradient is evaluated after the current velocity is applied
	- attempt to add correction factor
## Parameter Initialisation Strategies
![[Screenshot 2025-10-21 at 23.46.57.png|500]]
- larger initial weights will yield a stronger symmetry-breaking effect, helping to avoid redundant units
	- in recurrent networks can result in chaos 
		- such extreme sensitivity to small perturbations of the input that the behaviour of the deterministic forward propagation procedure appears random
	- may result in extreme values that cause the activation function to saturate, causing complete loss of gradient through saturated units
- one heuristic is to initialise the weights of a fully connected layer with $m$ inputs and $n$ outputs by sampling each weights from $U(-\frac 1 {\sqrt m}, \frac 1 {\sqrt m})$ while Glorot suggest using the normalised initialisation
$$
W_{i,j}\sim U(-\sqrt{\frac 6 {m+n}}, \sqrt{\frac 6 {m+n}})
$$
- sparse initialisation
	- each unit initialised to have exactly $k$ non zero weights
	- helps to achieve more diversity among the units at initialisation time
	- also imposes a very strong prior on the weights that are chosen to have large Gaussian values
- treat the initial scale of the weights for each layer as a hyperparameter
- approach for setting the biases must be coordinated with the approach for setting weights
	- setting the biases to zero is compatible with most weight initialisation schemes
	- some situations where we may set the biases to something else
		- if bias is for an output unit
		- want to choose the bias to avoid causing too much saturation at initialisation
			- not compatible with weight initialisation schemes that do not expect strong input from the biases
		- sometimes a unit controls whether other units are able to participate in a function
- another common parameter type is variance/precision parameter
	- can normally initialise variance parameters to 1 safely
- possible to initialise model parameters using machine learning
	- initialise a supervised model with the parameters learned by an unsupervised model trained on the same inputs
	- take someone else's model parameters 
## Algorithms with adaptive learning rates
### AdaGrad
![[Screenshot 2025-10-22 at 22.40.21.png|400]]
- individually adapts the learning rates of all model parameters by scaling them inversely proportional to the square root of the sum of all the historical squared values of the gradient 
	- parameters with largest partial derivative of loss have correspondingly rapid decrease in their learning rate
	- parameters with small partial derivative of loss have relatively small decrease in their learning rate
- training deep neural network models, the accumulation of squared gradients from the beginning of training can result in a premature and excessive decrease in the effective learning rate
- performs well for some but not all deep learning models
### RMSProp
![[Screenshot 2025-10-22 at 22.40.37.png|400]]
- modifies AdaGrad to perform better in the non-convex setting 
	- changes the gradient accumulation into an exponentially weighted moving average
- uses an exponentially decaying average to discard history from the extreme past so that it can converge rapidly after finding a convex bowl
- has been shown to be an effective and practical optimisation algorithm for deep neural networks
- currently one of the go-to optimisation methods
![[Screenshot 2025-10-22 at 22.46.04.png|400]]
### Adam
![[Screenshot 2025-10-24 at 23.34.04.png|400]]
- adaptive moments
- variant on the combination of RMSProp and momentum  with a few important distinctions
	- momentum is incorporated directly as an estimate of the first-order moment of the gradient
	- includes bias corrections to the estimates of both the first-order moments and the second-order moments to account for their initialisation at the origin
- unlike in Adam, the RMSProp second-order moment estimate may have high bias early in training
- Adam generally regarded as being fairly robust to the choice of hyperparameters, though the learning rate sometimes needs to be changed from the suggested default
### Choosing the right optimisation algorithm
- no single best algorithm
- most popular
	- SGD, SGD with momentum, RMSProp, RMSProp with momentum, AdaDelta, and Adam
## Approximate Second-Order Methods
- the only objective function we examine is the empirical risk
$$
J(\theta)= \mathbb E_{x,y \sim \hat p_{data}(x,y)}[L(f(x;\theta),y)]=\frac 1 m \sum_{i=1}^m L(f(x^{(i)}; \theta), y^{(i)})
$$
### Newton's Method
![[Screenshot 2025-10-24 at 23.41.44.png|400]]
- most widely used second-order method
- is an optimisation scheme base on using a second-order Taylor series expansion to approximate $J(\theta)$ near some point $\theta_0$, ignoring derivatives of higher order
- inverse hessian has to be computed at every training iteration, due to this only networks with a very small number of parameters can be practically trained via Newton's method
### Conjugate Gradients
![[Screenshot 2025-10-25 at 22.49.07.png|400]]
- method to efficiently avoid the calculation of the inverse Hessian by iteratively descending conjugate directions
- two popular methods for computing the $\beta _t$ are
![[Screenshot 2025-10-24 at 23.49.22.png|400]]
### BFGS
- Broyden-Fletcher-Goldfarb-Shanno algorithm attempts to bring some of the advantages of Newton's method without the computational burden
- unlike conjugate gradients the success of the approach is not heavily dependent on the line search finding a point very close to the true minimum along the line
- issue is it must store the inverse Hessian matrix making it impractical
	- Limited Memory BFGS tries to help this
## Optimisation strategies and meta-algorithms
### Batch Normalisation 
- is a method of adaptive reparametrisation, motived by the difficulty of training very deep models

316