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
- for the general case:
	$$
	\ln p(\boldsymbol{X}|\boldsymbol{\theta})=\ln\{\sum_{\boldsymbol{z}}p(\boldsymbol{X}, \boldsymbol{Z}|\boldsymbol{\theta})\}
	$$
	- $Z$ are hidden variables (i.e. not observed) also called latent variables
	- $\{X, Z\}$ is the complete data (assume that if we had the complete data then MLE would be easy)
	- $\{X\}$ is the incomplete data
### Decomposing the log-likelihood
- let $q(\boldsymbol{Z})$ be any distribution over the hidden variables
- we have the following key decomposition of the log-likelihood: $\ln p(\boldsymbol{X}|\boldsymbol{\theta})=\mathcal{L}(q, \boldsymbol{\theta})+KL(q||p)$ 
	- $\mathcal{L}(q,\boldsymbol{\theta})=\sum_{\boldsymbol{Z}}q(\boldsymbol{Z})\ln\{\frac{p(\boldsymbol{X}, \boldsymbol{Z}|\boldsymbol{\theta})}{q(\boldsymbol{Z})}\}$
	- $KL(q||p)=-\sum_{\boldsymbol{Z}}q(\boldsymbol{Z})\ln\{\frac{p(\boldsymbol{Z}|\boldsymbol{X}, \boldsymbol{\theta})}{q(\boldsymbol{Z})}\}$
		- $KL(p_1||p_2)$ denotes the Kullback-Leibler divergence between probability distributions $p_1$ and $p_2$ 
		- KL-divergence is important in e.g. information theory
		- bit like a distance between two distributions, but not a true distance since, for example, it is not symmetric
		- $KL(p_1||p_2)\geq 0$ and $KL(p_1||p_2)=0$ iff $p_1=p_2$
	- $KL(q||p)\geq 0$ for any choice of $q$, so $\mathcal{L}(q,\boldsymbol{\theta})\leq \ln p(\boldsymbol{X}|\boldsymbol{\theta})$ 
		- in the E-step we increase $\mathcal{L}(q,\boldsymbol{\theta})$ by updating $q$ (and leaving $\boldsymbol{\theta}$ fixed)
		- in the M-step we increase $\mathcal{L}(q,\boldsymbol{\theta})$ by updating $\boldsymbol{\theta}$ (and leaving $q$ fixed)
		- after the E-step we have $\mathcal{L}(q,\boldsymbol{\theta})=\ln p(\boldsymbol{X}|\boldsymbol{\theta})$ so that in the following M-step increasing $\mathcal{L}(q,\boldsymbol{\theta})$ will also increase $\ln p(\boldsymbol{X}|\boldsymbol{\theta})$
### E-step
$$
	\ln p(\boldsymbol{X}|\theta^{old})=\mathcal{L}(q, \theta^{old})+KL(q||p)
$$
- we update $q$ but leave $\theta^{old}$ fixed
- $KL(q||p)=0$ when $q=p$, so to maximise $\mathcal{L}(q,\theta^{old})$ we set $q(\boldsymbol{Z})=p(\boldsymbol{Z}|\boldsymbol{X},\theta^{old})$
	- this increases $\mathcal{L}(q,\theta^{old})$ but not $\ln p(\boldsymbol{X}|\theta^{old})$
![[Screenshot 2024-10-20 at 15.00.57.png|250]]




change $q$ so $\ln p(q|p)=0$, this raises $\mathcal{L}(q,\theta)$ 
