---
tags:
  - Lesson
---
## Laplace Prior - soft thresholding
- assume that the likelihood function is
$$
p(x|\theta) = \frac 1 {\sigma _n \sqrt{2\pi}} \exp -\frac{(x-\theta)^2}{2\sigma ^2_n}
$$
- prior pdf is
$$
p(\theta) = \frac{1}{\sigma \sqrt{2}}\exp - \frac{\sqrt 2 |\theta|}{\sigma}
$$
- using the [[The Maximum a Posteriori (MAP) Estimator]] we can get 
$$
\hat \theta = x - \sqrt 2 \frac{\sigma _n ^2 }{\sigma}sign(\theta)
$$
or 
$$
\hat \theta = sign(x)(|x| - \sqrt 2 \frac {\sigma _n ^2}{\sigma})_+, \; where (g)_+ = \begin{cases}
0, & g < 0 \\ g, & otherwise
\end{cases}
$$
![[Screenshot 2025-09-29 at 15.06.32.png|500]]
## Deep Image Prior (DIP)
- idea: A randomly initialised neural network can be used as handcrafted prior for solving imaging inverse problems
- not fully model based not fully neural network
	- middle ground between learning-based, data-driven methods, which use deep convolutional neural networks and classical model-based approaches involving handcrafted image priors
	- relies on both but doesn't need tonnes of data
![[Screenshot 2025-09-29 at 15.07.12.png|500]]
- start with sample of pure noise ($z$) that you pass through a neural network, you get $f_{\theta _0}(z)$. Take that output of the neural network together with the image you want to enhance. Calculate the distance between the neural network output and the image ($x_0$). Take the gradient of that distance and backpropogate it back in. You repeat this until you get a very similar image to that which you wanted to de-noise 
	- you need to find the right moment to stop, stop in the bottom of the curve before you start reconstructing noise
$$
y = Hx + n, n \sim N(0, \sigma ^2 l)
$$
- variational formula
$$
\hat x = \arg \min _x [l(y,x)+\lambda \varphi (x)]
$$
- for a surjective mapping $g:\theta \rightarrow x$ the following minimisation could be attempted instead
$$
\hat \theta= \arg \min _\theta [l(y,g(\theta)) + \lambda \varphi (g(\theta))]
$$
- assuming a good choice of $g$, DIP gets rid of the prior and puts in a neural network $f_\theta (z)$ 
$$
\hat \theta= \arg \min _\theta [l(y,f_\theta (z))]
$$
- where $f_\theta$ is a DNN initialised randomly, while the input $z$ is AWGN and fixed, we can write for DIP
$$
\hat \theta = \arg \min _\theta ||y-Hf_\theta (z)||_2^2, \; s.t. \hat x = f_{\hat \theta}(z)
$$
- Applications
	- denoising (removing salt and pepper)
	- inpainting (has sections of white where photo is not present)
