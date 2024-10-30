---
tags:
  - sequential_data
---
- A state space model
- $\boldsymbol{z}_n$ are latent (unobserved) discrete state variables
- $\boldsymbol{x}_n$ are observations, which may be discrete or continuous values depending on the application
![[Screenshot 2024-10-28 at 10.44.57.png|150]]
### Sequence Labelling for Text
- sequence labelling: classifying data points in a sequence
	- e.g. classifying words in a text document into grammatical categories such as noun, verb, adjective, etc
	- this is called part-of-speech (POS) tagging and is used by natural language understanding systems e.g. to extract facts and events from text data
	![[Screenshot 2024-10-28 at 10.49.56.png|200]]
	- english language makes sequential text difficult as it has a lot of ambiguity when it comes to nouns, verbs, etc
- we use an HMM model for human action recognition as actions typically follow a temporal sequence
- HMMs can be used for different goals:
	- inferring the latent states (sequence labelling)
	- predicting the next latent state
	- predicting the next observation
- HMMs can be used with different levels of supervision:
	- **Supervised**: latent states are given in the training set
	- **Unsupervised**: no labels for the latent states, so the model seeks an assignment that best explains the observations given the model 
	- **Semi-supervised**: some labels are given, but the model is learned over both labelled and unlabelled data
		- avoids overfitting to a very small labelled dataset while identifying latent states that follow the desired labelling scheme
- the probabilistic model of the HMM is made up of two main parts:
	- **The transition distribution**: can be represented as a transition matrix and models the dependencies between the latent states
		- probability of $\boldsymbol{z}_n$ depends on the previous state: $p(\boldsymbol{z}_n|\boldsymbol{z}_{n-1})$
		- given $K$ labels (state values), we can write all the values of $p(\boldsymbol{z}_n=k|\boldsymbol{z}_{n-1=l})$ in a transition matrix, $\boldsymbol{A}$
			- rows correspond to values of the previous state, $\boldsymbol{z}_{n-1}$
			- columns are values of the current state, $\boldsymbol{z}_n$
			![[Screenshot 2024-10-28 at 11.03.12.png|200]]
		- a vector of probabilities $\pi$ is used for $\boldsymbol{z_1}$ (to give the initial state probabilities), this us does to it having no predecessor
		- a transition matrix for a mixture model would have all rows looking the same as data is independent
	- **The emission distributions**: models the observations given each latent state value
		- distribution over the observed variables, $p(\boldsymbol{x}_n|\boldsymbol{z}_n, \phi)$, where $\phi$ are parameters of the distributions, e.g.
			- real-valued observations may use Gaussian emissions
			- if there are multiple observations, we may use a multivariate Gaussian
			- discrete observations may use a categorical distribution
		- for each observation there are $K$ values of $p(\boldsymbol{x}_n|\boldsymbol{z}_n, \phi)$, one for each possible value of the unobserved $\boldsymbol{z}_n$
- the complete HMM can be defined by the joint distribution over observations and latent states:
	$$
	p(\boldsymbol{X},\boldsymbol{Z}|\boldsymbol{A},\pi,,\phi)=p(\boldsymbol{z}_1|\pi)\prod_{n=2}^Np(\boldsymbol{z}_n|\boldsymbol{z}_{n-1},\boldsymbol{A})\prod_{n=1}^Np(\boldsymbol{x}_n|\boldsymbol{z}_n,\phi)
	$$
	- $\boldsymbol{A}, \pi$ and $\phi$ are parameters that must be learned or marginalised
	- generative model: think of generating each of the state variables $\boldsymbol{z}_n$ in turn, then generating the observation $\boldsymbol{x}_n$ for each generated state
	- it is ancestral sampling (see [[univariate sampling]] notes)
### EM for HMMs
- EM is for estimating when we don't have the $\boldsymbol Z$ only the $\boldsymbol X$ 
- we want to use maximum likelihood to estimate the HMM parameters:
	- $\boldsymbol{A}$ - transition matrix
	- $\pi$ - initial state probabilities
	- $\phi$ - parameters of the emission distributions
- examine the unsupervised case where the sequence of states $\boldsymbol{Z}$ is not observed
	- $\ln p(\boldsymbol{X}|\boldsymbol{A},\pi,\phi)=\ln\sum_{\boldsymbol{Z}}\{p(\boldsymbol{z}_1|\pi)\prod_{n=2}^Np(\boldsymbol{z}_n|\boldsymbol{z}_{n-1}, \boldsymbol{A})\prod_{n=1}^Np(\boldsymbol{x}_n|\phi, \boldsymbol{z}_n)\}$
- as with GMMs, there is no closed-form solution to the MLE, we turn to [[EM algorithm]]
- unlike GMM, the likelihood doesn't factorise over the data points:
	- $\ln p(\boldsymbol{X}|\boldsymbol{A},\pi,\phi)=\ln\sum_{\boldsymbol{Z}}\{p(\boldsymbol{z}_1|\pi)\prod_{n=2}^Np(\boldsymbol{z}_n|\boldsymbol{z}_{n-1}, \boldsymbol{A})\prod_{n=1}^Np(\boldsymbol{x}_n|\phi, \boldsymbol{z}_n)\}$
	- the distribution of $\boldsymbol{z}_n$ depends on $\boldsymbol{z}_{n-1}$, which also depends on $\boldsymbol{z}_{n-2...}$
	- can't just sum over the values of $z_n$ independently for each data point
	- we have to sum over all $K^N$ possible sequences $\boldsymbol{Z}$
- EM, maximising the log likelihood of a HMM
	- first define $Q(\boldsymbol{\theta}|\boldsymbol{\theta}^{old})=\sum_{\boldsymbol Z}p(\boldsymbol Z|\boldsymbol X, \boldsymbol{\theta}^{old}\ln p(\boldsymbol{X}, \boldsymbol{Z}|\boldsymbol{\theta})$
		1. initialise the parameters with a random guess: $\boldsymbol{\theta}^{old}=\{\boldsymbol{A},\pi,\phi\}$
		2. **E-step**: use $\boldsymbol{\theta}^{old}$ to compute expectations over $\boldsymbol{Z}$ required to compute $Q(\boldsymbol{\theta}|\boldsymbol{\theta}^{old})$ 
		3. **M-step**: choose the values of $\boldsymbol{\theta}=\{\boldsymbol{A}, \pi,\phi\}$ that maximise $Q(\boldsymbol{\theta}|\boldsymbol{\theta}^{old})$
		4. set $\boldsymbol{\theta}^{old}=\boldsymbol{\theta}$
		5. repeat steps 2-4 until convergence
- **E Step**:
	- compute expectations of the latent states and pairs of latent states
	- probability is just a special type of expectation: one for a binary random variable
	- Responsibilities: $\gamma(z_{nk})=p(z_n=k|\boldsymbol X, \boldsymbol{\theta}^{(old)})$
	- State pairs: $\xi(z_{n-1,j},z_{nk})=p(z_{n-1}=j,z_n=k|\boldsymbol X, \boldsymbol{\theta}^{(old)})$
	- compute efficiently we need the forward-backward algorithm

	- find posterior distribution of the latent variables $p(\boldsymbol Z| \boldsymbol X, \boldsymbol{\theta}^{old})$
		- note we don't compute and store the entire distribution $p(\boldsymbol Z| \boldsymbol X, \boldsymbol{\theta}^{old})$ only the expectations of the things we need for the subsequent M step
- **M Step**:
	- $\pi_k=\gamma(z_{1k})$
	- $A_{jk}=\sum_{n=2}^N\xi(z_{n-1,j},z_{nk})/\sum_{n=2}^N\gamma(z_{n-1,j})$
	- $\phi_k$: parameters of posterior emission distributions, with observations weighted by responsibilities, $\gamma(z_{nk})$
		- if we have Gaussian emissions, the equations are the same as for GMM
		- discrete observations with value $i$:
		$$
		\phi_{ki}=p(x_n=i|z_n=k)=\frac{\sum_{n=1}^N\gamma(z_nk)[x_n=i]}{\sum_{n=1}^N\gamma(z_{nk})}
		$$
## Forward-backward Algorithm
![[Forward-backward Algorithm]]


once we're done with our training there are two things you might want to do with a HMM you might want to:
- workout the most probable state (most probable tag for a word)
- workout the most probable state trajectory (most probable sequence of tags)
	- use the [[Viterbi Algorithm]] to do this