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


## Part 2
## Generate Image (Sampling Phase)
- each step removes a small amount of noise, guided by the model's prediction
- after hundreds of steps, the model reconstructs a sharp, realistic image
- conditioning (like text prompts) guides what kind of image is formed
## Considerations
### Noise Schedule
- parameters $\beta_t$ and $\sigma_t ^2$ control the variance of the forward diffusion and reverse denoising processes, respectively
- often a linear schedule is used for $\beta_t$, and $\sigma_t^2$ is set equal to $\beta_t$
	- for small images the image becomes almost pure Gaussian noise very early in the diffusion process
---
## Why
![[Screenshot 2025-10-22 at 09.16.09.png|500]]
- stable and high quality: Less prone to artefacts than GANs
- Probabilistic foundation: Based on modelling data distribution through noise transitions
- controllable generation: can guide results with text prompts, class labels, or images
---
![[CLIP (Contrastive Language-Image Pre-Training)]]
- ViT uses attention to see what are the "key words" of the image
	- image is split into Patch + Position embedding and this is passed in 
	- good to find the important parts of an image
**missed hippo on stable diffusion v3**

- ChatGPT uses DALL-E 3