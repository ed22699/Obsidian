---
tags:
  - sequential_data
---
Dynamic programming problem
- forward pass: compute the probability of the most likely sequence that leads to each possible state at time $n$
	1. $\omega(z_{1k})=\ln\pi_k+\ln p(\boldsymbol x_1|z_1=k)$
	2. for $n=2$ to $N$ compute for each state value $k$:
		1. $\omega(z_{nk})=\max_l \{\omega(z_{n-1,l})+\ln p(z_n=k|z_{n-1}=l)\}+\ln p(\boldsymbol x_n|z_n=k)$
		2. $\phi(z_{nk})=\arg\max_l\{\omega(z_{n-1,l})+\ln p(z_n=k|z_{n-1}=l)\}+\ln p(\boldsymbol x_n|z_n=k)$
		3. passes messages from the start of the sequence to the end
- backward pass: starting with the most likely final state and recursing backwards, choose the previous state $n-1$ that makes the chosen state at $n$ most likely