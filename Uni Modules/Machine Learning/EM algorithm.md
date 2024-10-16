---
tags:
  - Lesson
  - em_algorithm
---
# Setting derivatives to zero
- $\boldsymbol{\mu}_k=\frac 1 {N_k}\sum_{n=1}^N\gamma(z_{nk})\boldsymbol{x}_n$
- $\boldsymbol{\Sigma}_k=\frac 1{N_k}\sum_{n=1}^N\gamma(z_{nk})(\boldsymbol{x}_n - \boldsymbol{\mu}_k)(\boldsymbol{x}_n-\boldsymbol{\mu}_k)^T$
- $\pi_k=\frac{N_k}N$
- where $\gamma(z_{nk})=p(z_k=1|\boldsymbol{x_n})$ and $N_k=\sum_{n=1}^N\gamma(z_{nk})$ 
# EM for Gaussian mixtures
![[Screenshot 2024-10-15 at 11.55.49.png|300]]
- to initialise the EM algorithm we choose starting values for $\boldsymbol{\mu}, \boldsymbol{\Sigma}$ and $\pi$
**E Step**
- compute the values for the responsibilities $\gamma(z_{nk})$ given the current parameter values:
	$$
	\gamma(z_{nk})=\frac{\pi_k\mathcal{N}(\boldsymbol{x}_n|\boldsymbol{\mu}_k, \boldsymbol{\Sigma}_k)}{\sum_{j=1}^K\pi_j\mathcal{N}(\boldsymbol{x}_n|\boldsymbol{\mu}_j, \boldsymbol{\Sigma}_j)}
	$$
	- is just Bayes theorem
	- $p(z_k=1|\boldsymbol{x}_n)=\frac{p(z_k=1)p(\boldsymbol{x}_n|z_k=1)}{p(\boldsymbol{x}_n)} = \frac{p(z_k=1)p(\boldsymbol{x}_n|z_k=1)}{\sum_{j=1}^K p(z_j=1)p(\boldsymbol{x}_n|z_j=1)}$ (same as the above equation just with different notation)
**M step**
- re-estimate the parameter using the current responsibilities:
	- $\boldsymbol{\mu}_k^{new}=\frac 1 {N_k}\sum_{n=1}^N\gamma(z_{nk})\boldsymbol{x}_n$
	- $\boldsymbol{\Sigma}_k^{new}=\frac 1{N_k}\sum_{n=1}^N\gamma(z_{nk})(\boldsymbol{x}_n - \boldsymbol{\mu}_k^{new})(\boldsymbol{x}_n-\boldsymbol{\mu}_k^{new})^T$
	- $\pi_k^{new}=\frac{N_k}N$
>[!note]
E and M are iterated, each time converging more onto clusters

## Why does EM work?
change $q$ so $\ln p(q|p)=0$, this raises $\mathcal{L}(q,\theta)$ 
