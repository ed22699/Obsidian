---
tags:
  - sequential_data
---
- instance of the more general max-sum algorithm to find the most likely sequence of hidden states
Dynamic programming problem
- forward pass: compute the probability of the most likely sequence that leads to each possible state at time $n$
	1. $\omega(z_{1k})=\ln\pi_k+\ln p(\boldsymbol x_1|z_1=k)$
	2. for $n=2$ to $N$ compute for each state value $k$:
		1. $\omega(z_{nk})=\max_l \{\omega(z_{n-1,l})+\ln p(z_n=k|z_{n-1}=l)\}+\ln p(\boldsymbol x_n|z_n=k)$
		2. $\phi(z_{nk})=\arg\max_l\{\omega(z_{n-1,l})+\ln p(z_n=k|z_{n-1}=l)\}+\ln p(\boldsymbol x_n|z_n=k)$
		3. passes messages from the start of the sequence to the end
- backward pass: starting with the most likely final state and recursing backwards, choose the previous state $n-1$ that makes the chosen state at $n$ most likely
	1. most likely final state: $\hat z_N=\arg\max_w(z_{Nk})$
	2. for $n=N-1$ to $1:\hat z_n=\psi(z_{n+1,\hat z_{n+1}})$
- there are multiple paths leading to each possible state at each step $n$. We keep only the path with the highest probability, so we don't have to compute the likelihood of every complete path from $1$ to $N$