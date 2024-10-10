---
tags:
  - markov_chain_monete_carlo
---
- some mechanism for sampling from any univariate distribution
- if a multivariate distribution is described by a Bayesian network then we can use ancestral sampling to sample a joint instantiation of the variables
## Ancestral Sampling
- need to ensure that we sample all parent node values before sampling the value of the child node (always possible due to acyclicity)
![[Screenshot 2024-10-10 at 14.07.33.png|100]]
$p(A,B,C,D,E)=p(A)p(B)p(C|A,B)p(D|C)p(E|B,C)$
- first we sample values for $A$ and $B$, suppose we get the values $A=0,B=1$ we can then sample a value for $C$ from the conditional distribution $P(C|A=0,B=1)$ and so on
## Sampling from marginal and conditional distributions
- can approximate any marginal distribution by sampling full joint instantiations (by e.g. ancestral sampling) and then only keeping the value of the variables in the marginal
- use rejection sampling to sample from conditional distributions
	- e.g. to sample from $P(B,D|E=1)$ we sample from the marginal distribution $P(B,D,E)$ and throw away those sample where $R\neq 1$
	- typically inefficient