---
tags:
  - Lesson
---
## Distribution of MNIST data
- natural images do not scatter randomly across the pixel space; instead, tehy concentrate on a complex, low-dimensional manifold embedded in a high-dimensional space
- a generative model learns to generate images that looks like it came from the real data
- notations
	- $q(x)$ or $p_{data}(x)$: the probability density function of the distribution of real data
	- $p_{\theta}(x)$: the pdf of a learned distribution with parameters $\theta$
![[Screenshot 2025-10-20 at 12.13.53.png|500]]
- for a real sample (image) $x_0, p_\theta(x_0)$ represents the *likelihood* of that sample under that model parameterised by $\theta$
- in practical, training a generative model means adjusting $\theta$ so that real samples $x_0$ get higher likelihood
![[Screenshot 2025-10-20 at 12.18.40.png|500]]
- why choose multi-step generation?
	- more like the drawing process of a human
		- works similar to the human brain, broken into step by step, making the generation much easier
![[Screenshot 2025-10-20 at 12.20.15.png|400]]
## Diffusion Processes
- diffusion model is a *parameterised Markov chain* trained using variational inference to produce samples matching the data after finite time ([[Markov Chain]])
	- transitions of this chain are learned to reverse a diffusion process, which is a Markov chain that gradually adds noise to the data in the opposite direction of sampling until signal is destroyed
![[Screenshot 2025-10-20 at 12.25.00.png|300]]
- denoising diffusion models consists of two processes:
### Forward Diffusion
![[Forward Diffusion]]
### Backward Denoising
![[Backward Denoising]]
## Training and Sampling
![[Screenshot 2025-10-20 at 12.53.13.png|500]]