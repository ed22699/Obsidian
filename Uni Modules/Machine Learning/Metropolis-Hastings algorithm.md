---
tags:
  - markov_chain_monete_carlo
---
- define a single transition probability distribution for a homogeneous [[Markov Chain]]
- let the current state be $\boldsymbol{z}^{(\tau)}$. When using the MH algorithm sampling the next state happens int two stages
	1. we generate a value $\boldsymbol{z}^*$ by sampling fro a proposal distribution $q(\boldsymbol{z}|\boldsymbol{z}^{(\tau)})$ 
	2. we then accept $\boldsymbol{z}^*$ as the new state with a certain acceptance probability in which case $\boldsymbol{z}^{(\tau +1)}=\boldsymbol{z}^{(\tau)}$ 
- let $p(\boldsymbol{z})$ be the target distribution
- acceptance probability is: 
$$
A(\boldsymbol{z}^*, \boldsymbol{z}^{(\tau)}=\min (1, \frac{p(\boldsymbol{z}^*)q(\boldsymbol{z}^{(\tau)}|\boldsymbol{z}^*)}{p(\boldsymbol{z}^{(\tau)})q(\boldsymbol{z}^*|\boldsymbol{z}^{(\tau)})})
$$
- if $p(\boldsymbol{z})=\frac{\tilde{p}(\boldsymbol{z})}{Z}$ then we have 