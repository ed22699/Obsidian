---
tags:
  - markov_chain_monete_carlo
---
## Use in sampling for modelling data (MCMC, special case)
- first-order Markov chain is defined to be a series of random variables $\boldsymbol{z}^{(1)},...,\boldsymbol{z}^{(M)}$ such that the following conditional independence property holds for $m \in \{1,...,M-1\}$ 
	- $\boldsymbol{z}^{(m)}$ often represents the $m^{th}$ state of some dynamic system so that $p(\boldsymbol{z}^{(m+1)}|\boldsymbol{z}^{(m)})$ is the state transition probability
	- if $p(\boldsymbol{z}^{(m+1)}|\boldsymbol{z}^{(m)})$ is the same for all $m$ then the chain is homogeneous
	- we also need an initial distribution $p(\boldsymbol{z}^{(1)})$
- here's the Bayesian network representation of a Markov chain where $M=4$
![[Screenshot 2024-10-10 at 14.27.24.png|200]]
- Markov Chain sampling is a special case of ancestral sampling
- a Markov chain defines a sequence of marginal distributions (for the example above these are $P(\boldsymbol{z_1})$, $P(\boldsymbol{z_2})$, $P(\boldsymbol{z_3})$ and $P(\boldsymbol{z_4})$)
## To show dependencies
$1^{st}$ order Markov chain, $p(\boldsymbol{x}_n|\boldsymbol{x}_1,...,\boldsymbol{x}_{n-1})=p(\boldsymbol{x}_n|\boldsymbol{n}_{n-1})$
![[Screenshot 2024-10-28 at 10.21.27.png|150]]
- $p(\boldsymbol{x}_1,...,\boldsymbol{x}_N)=p(\boldsymbol{x}_1)\prod_{n=2}^N p(\boldsymbol{x}_n|\boldsymbol{x}_{n-1})$
### Homogeneous Markov Chains
- in a stationary distribution the probability distribution remains the same over time, this leads to a homogeneous Markov chain (e.g. parameter of the distribution remain the same while the data evolves)
	- this in in contrast with non-stationary distributions that change over time
### Higher-Order Markov Models
- sometimes necessary to consider earlier observations using a higher-order chain, however, the number of parameters increases with the order of the Markov chain, meaning higher-order models are often impractical
- $2^{nd}$ order Markov chain, $p(\boldsymbol{x}_n|\boldsymbol{x}_1,...,\boldsymbol{x}_{n-1})=p(\boldsymbol{x}_n|\boldsymbol{x}_{n-1},\boldsymbol{x}_{n-2})$
	![[Screenshot 2024-10-28 at 10.30.54.png|140]]
	-  $2^{nd}$ order Markov Chain says the information on the last point isn't enough to predict the next point, we also need the point before the previous
