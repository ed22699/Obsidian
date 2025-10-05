---
tags:
  - model_based_deep
---
## RED: Regularisation by Denoising
$$
y = Hx +n, n \sim N(0, \sigma ^2 I)
$$
- the variational formulation:
$$
\hat x = \arg \min _x [l(y,x)+\lambda \varphi (x)]
$$
- *Idea*: use the following as the regularisation function
$$
\varphi (x) = \frac 1 2 x^T (x-g(x))
$$
- $g$ can be a denoiser of your choice
- under mild conditions on $g$, two highly beneficial properties can be obtained
	- the gradient of $\varphi$ w.r.t. $x$ is simple and given $\nabla \varphi(x)=x-g(x)$ which avoids differentiating the denoiser function
	- $\varphi$ is a convex functional

## DeepRED: DIP Powered by RED
- *Idea*: merge DIP and RED, obtaining the following
$$
\arg \min_{x,\theta}\frac 1 2 ||y-Hf_\theta (z)||_2^2 + \frac \lambda 2 x^T (x-g(x)), \; s.t. \;x=f_{\theta}(z)
$$
- whole optimisation only w.r.t. the parameters $\theta$, as in DIP
$$
\arg \min \frac 1 2 ||y-Hf_\theta (z)||_2^2 + \frac \lambda 2 f_{\theta}(z)^T(f_\theta (z)-g(f_{\theta} (z)))
$$
- requires differentiating the denoising function $g$ when back propagating over $f$. Actual solution comes from ADMM
- Augmented Lagrangian
$$
\arg \min_{x, \theta}\frac 1 2 ||y-Hf_\theta (z)||_2^2 + \frac \lambda 2 x^T (x-g(x))+\frac \mu 2 ||x-f_\theta (z) - u||_2^2
$$
- where 
	- $u$ is the Lagrangian multiplier vector for the set of equality constraints
	- $\mu$ is a free parameter
- basically just adds the RED equation to the [[Deep Image Prior (DIP)]] formula
