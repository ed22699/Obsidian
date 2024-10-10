---
tags:
  - markov_chain_monete_carlo
---
- first-order Markov chain is defined to be a series of random variables $\boldsymbol{z}^{(1)},...,\boldsymbol{z}^{(M)}$ such that the following conditional independence property holds for $m \in \{1,...,M-1\}$ 
	- $\boldsymbol{z}^{(m)}$ often represents the $m^{th}$ state of some dynamic system so that $p(\boldsymbol{z}^{(m+1)}|\boldsymbol{z}^{(m)})$ is the state transition probability
	- if $p(\boldsymbol{z}^{(m+1)}|\boldsymbol{z}^{(m)})$ is the same for all $m$ then the chain is homogeneous
	- we also need an initial distribution $p(\boldsymbol{z}^{(1)})$
- here's the Bayesian network representation of a Markov chain where $M=4$
![[Screenshot 2024-10-10 at 14.27.24.png|200]]
- Markov Chain sampling is a special case of ancestral sampling
- a Markov chain defines a sequence of marginal distributions (for the example above these are $P(\boldsymbol{z_1})$, $P(\boldsymbol{z_2})$, $P(\boldsymbol{z_3})$ and $P(\boldsymbol{z_4})$)