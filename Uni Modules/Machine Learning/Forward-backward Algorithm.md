---
tags:
  - sequential_data
---
example of the sum-product algorithm used in the E-step
- forward pass computes for each time-step $n$ and state value $k$:
	- $\alpha(z_{nk})=p(\boldsymbol x_1,..., \boldsymbol x_n, z_n=k|\pi,\boldsymbol A, \phi)$
	- $= p(\boldsymbol x_n|z_n=k,\phi_k)\sum_{l=1}^KA_{lk}\alpha(z_{n-1,l})$
- backwards pass computes:
	- $\beta(z_{nk})=p(\boldsymbol x_{n+1},...,\boldsymbol x_N|z_{n}=k, \boldsymbol A, \phi)$
	- $=\sum_{l=1}^KA_{kl}p(\boldsymbol x_{n+1}|z_{n+1}=l, \phi_l)\beta(z_{n+1,l})$
- use the computed $\alpha$ and $\beta$ terms to compute our expectations over $\boldsymbol z$
	- before: $\tilde{\xi}(z_{n-1,l},z_{nk})=p(\boldsymbol x_1, ..., \boldsymbol x_{n-1}, z_{n-1}=l|\boldsymbol A,\pi,\phi)$
	- current: $p(z_n=k|z_{n-1}=l,\boldsymbol A)p(\boldsymbol x_n|z_n=k,\phi)$
	- after: $p(\boldsymbol x_{x+1},..., x_N|z_n=k,\boldsymbol A,\phi)$
	$$
	\tilde{\xi}(z_{n-1,l},z_{nk})=\alpha(z_{n-1,l})A_{lk}p(\boldsymbol x_n|z_n=k,\phi)\beta(z_{nk})
	$$
- $\xi(z_{n-1,l},z_{nk})=\tilde{\xi}(z_{n-1,l},z_{nk})/\sum_{l=1}^K\sum_{k=1}^K\tilde{\xi}(z_{n-1,l},z_{nk})$
- $\gamma(z_{nk})=\sum_{l=1}^K\xi(z_{n-1,l},z_{nk})$
**Formula**
1. initialise the parameters with a random guess: $\boldsymbol{\theta}^{old}=\{\boldsymbol A,\pi,\phi\}$
2. **E-step** using $\boldsymbol{\theta}^{old}$
	1. run forward pass to compute $\alpha(z_{nk})$
	2. run backward pass to compute $\beta(z_{nk})$
	3. use $\alpha(z_{n-1,l},z_{nk})$ and $\beta(z_{nk})$ to compute $\xi(z_{n-1,l},z_{nk})$ and $\gamma(z_{nk})$
3. **M-step** using $\xi(z_{n-1,l},z_{nk})$ and $\gamma(z_{nk})$, update $\boldsymbol \theta =\{\pi, \boldsymbol A, \phi\}$
4. Set $\boldsymbol \theta^{old}=\boldsymbol \theta$
5. Repeat steps 2-4 until convergence
- by summing inside each forward and backward computations, we now have an algorithm that is linear $O(N)$ rather than exponential $O(K^N)$ in the sequence length
