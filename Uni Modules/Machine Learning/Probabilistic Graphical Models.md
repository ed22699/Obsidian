---
tags:
  - Lesson
  - probabilistic_graphical_models
---
**Chain Rule**: $P(x_1,...x_n)=P(x_1)P(x_2|x_1)...P(x_n|x_1,...,x_{n-1})$
- with conditional independence: $P(x_3|x_1,x_2)=P(x_3|x_2)$
	- distribution $P$, $x_3$ is independent of $x_1$ conditional on $x_2$
	- so $P(x_1,...,x_n)=P(x_1)P(x_2|x_1)P(x_3|x_2)$
- Probabilistic graphical models (PGMs) provide a graphical representation of how a joint distribution factorises when there are conditional independence relations
## Bayesian Networks
- most commonly used PGM
- $P(x_1,...,x_n)=P(x_1)P(x_2|x_1)P(x_3|x_2)$ $\Rightarrow$ ![[Screenshot 2024-10-07 at 10.42.00.png|120]]
- for a distribution with no conditional independence relations a suitable BN would be $P(x_1,...,x_n)=P(x_1)P(x_2|x_1)P(x_3|x_1, x_2)$ $\Rightarrow$  ![[Screenshot 2024-10-07 at 10.43.59.png|120]]
	- if theres an arrow from $A$ to $B$ then $A$ is a parent of $B$ and $B$ is a child of $A$
	- $pa_k$: parents of node $x_k$
		- directed acyclic graph (DAG) determines $pa_k$ for each node $x_k$ in that DAG
	- a Bayesian network with parents sets $pa_k$ for random variables $x_1,...,x_K$ represents a joint distribution which factorises as follows: $p(\boldsymbol{x})=\Pi_{k=1}^Kp(x_k|pa_k)$ 
- for a BN to represent a given joint distribution we need to specify
	1. the DAG (structure of the BN)
	2. the conditional probability distributions $p(x_k|pa_k)$ (parameters of BN)
- a given DAG represents a set of joint distributions
	- each distribution in the set corresponds to a choice of values for the conditional distributions $p(x_k|pa_k)$
### Representing a Machine Learning Model
- to represent a machine learning model with a Bayesian approach we have to define a prior probability distribution over parameters which represent our beliefs about their values prior to observing the data
$$
p(\boldsymbol{t}, \boldsymbol{w})=p(\boldsymbol{w})\Pi_{n=1}^{N}p(t_n|\boldsymbol{w})
$$
- $\boldsymbol{w}$ is the vector of polynomial coefficients
- $\boldsymbol{t}$ is the observed output data
![[Screenshot 2024-10-07 at 11.00.43.png|200]]
#### Plate notation
![[Screenshot 2024-10-07 at 11.00.43.png|120]] $=$ ![[Screenshot 2024-10-07 at 11.02.21.png|120]]
- the plate around $t_n$, represents a set of nodes $t_1,...,t_N$ all of which have $\boldsymbol{w}$ as their single parent


A full Bayesian polynomial regression model contains:
1. the input data $\boldsymbol{x}=(x_1,...,x_N)^T$
2. the observed outputs $\boldsymbol{t}=(t_1,...,t_N)^T$
3. the parameter vector $\boldsymbol{w}$
4. a hyperparameter $\alpha$ 
	- don't care how $\boldsymbol{x}$ is distributed and we would probably just set $\alpha$ to some value
5. the noise variance $\sigma^2$
- we would typically consider $\boldsymbol{x}$, $\alpha$ and $\sigma^2$ as parameters of the model rather than random variables
- useful to represent these in the BN
![[Screenshot 2024-10-07 at 11.17.18.png|200]]
#### Example
![[Screenshot 2024-10-07 at 11.22.40.png|300]]
### Naive Bayes 
in naive Bayes model for classification the observed variables $\boldsymbol{x}=(x_1,...,x_D)$ are assumed independent conditional on the class variable $\boldsymbol{z}$:
$$
P(\boldsymbol{x},\boldsymbol{z})=P(\boldsymbol{z})P(\boldsymbol{x}|\boldsymbol{z})=P(\boldsymbol{z})\Pi_{i=1}^DP(x_i|\boldsymbol{z})
$$
**Standard Regression**:
- $P(\theta,y)=P(\theta)\Pi_{i=1}^kP(y_i|\theta$ $\Rightarrow$ ![[Screenshot 2024-10-07 at 11.30.12.png|120]]
**Separate Regressions**:
- $P(\theta, y)=\Pi_{i=1}^kP(y_i|\theta_i)P(\theta_i)$ $\Rightarrow$ ![[Screenshot 2024-10-07 at 11.33.14.png|120]]
**Hierarchical Regression**:
- $P(\theta,y,\mu,\sigma^2)=P(\mu, \sigma^2)\Pi_{i=1}^kP(y_i|\theta_i)P(\theta_i|\mu,\sigma^2)$ $\Rightarrow$ ![[Screenshot 2024-10-07 at 11.35.49.png|120]]
## Conditional Independence 
- a random variable $x$ is independent of another random variable $y$ conditional on a set of random variables $S$ iff: $P(x,)
