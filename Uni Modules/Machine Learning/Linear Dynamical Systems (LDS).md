---
tags:
  - Lesson
  - LDS
---
Similar to [[Hidden Markov Models (HMMs)]]
- HMM assumes discrete latent states, LDS assume states have continuous values
- both have same graphical model
	![[Screenshot 2024-11-13 at 11.24.14.png|200]]
- inference has same form as for HMM, but when marginalising $z_{n-1}$ and $z_{n+1}$ we take integrals instead of sums
- Motivations:
	- noisy sensors: inferring the true sequence of states from observations with Gaussian noise
	- tracking: predicting the next movement and tracing the path from noisy observations
## Transition and Emission Distributions for LDS
- $p(z_1)=\mathcal N(z_1|\mu_0,V_0)$
- $p(z_n|z_{n-1})=\mathcal N(z_n|Az_{n-1}, \Gamma)$
- $p(x_n|x_n)=\mathcal N(x_n|Cx_n,\Sigma)$
	- means of both distributions are linear functions of the latent states
	- choice of distributions ensures that the posteriors are also Gaussians with updated parameters
	- means that $O(N)$ inference can still be performed using the sum-product algorithm
## Inference for the LDS
- Kalman filter = forward pass of sum-product for LDS
	- $\alpha(z_n)=\mathcal N(x_n|Cz_n,\Sigma)\int\mathcal N(z_n|Az_{n-1},\Gamma)\alpha(z_{n-1})dz_{n-1}$
	- normalising results in a Gaussian-distributed variable, whose parameters can be computed efficiently: $\hat \alpha(z_n)=p(z_n|x_1,...,x_n)=\mathcal N(z_n|\mu_n,V_n)$
		- $\mu_n$ is a function of $\mu_{n-1}, x_n, A$ and $C$
		- $V_n$ is a function of $V_{n-1}, \Sigma, A, \Gamma$ and $C$
	- can view each forward step as predicting $z_n$ based on the distribution over $z_{n-1}$, then correcting that prediction given the new observation $x_n$
- Kalman smoother = backward pass of sum-product for LDS
	- also follows that of the HMM: messages are passed from the final state to the start of the sequence
- no need for an analogue of Viterbi: the most likely sequence is given by the individually most probable states, so we get this from the Kalman equations
