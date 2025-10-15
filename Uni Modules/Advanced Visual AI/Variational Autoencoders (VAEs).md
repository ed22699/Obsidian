---
tags:
  - generative_ai
---
![[Screenshot 2025-10-13 at 12.22.08.png|400]]
- assume it follows a normal distribution
	- you have to define how many $\mu$ and $\sigma$ will be used in the autoencoder in order to compute the latent samples
![[Screenshot 2025-10-13 at 12.22.55.png|400]]
- regularisation term is there to smooth the reconstruction loss
- we calculate the distance between the density distribution between the encoder and the fixed prior
- the $L(\phi, \theta, x)$ is the evidence lower bound (ELBO) Loss
## VAE Optimisation
- Priors on latent distribution
$$
D(q_{\phi}(z|x)||p(z)) = \frac 1 2 \sum_{j=0}^{k-1}(\sigma_j^2 +\mu _j ^2 - 1 -\log \sigma _j ^2)
$$
- for the prior, the common choice is to assume Normal Distribution
$$
p(z) = \mathcal N (\mu = 0, \sigma ^2 = 1)
$$
- encourages encoding to be normally distributed around the centre of the latent space
- penalises the network for introducing bias (e.g. clustering the points in specific region)
## Kullback-Leibler (KL) Divergence
- measures how one probability distribution diverges from another
$$
D_{KL}(P||Q)= \sum P(x)\log [\frac{P(x)}{Q(x)}]
$$
![[Screenshot 2025-10-13 at 12.33.51.png|400]]
- goal is to train to try and align between the two distributions
![[Screenshot 2025-10-13 at 12.36.09.png|500]]
- properties achieved through regularisation
	- *Continuity*: small changes in the latent space (i.e. the space of the encoded latent variables $z$) should correspond to small and smooth changes in the generated output data
	- *Completeness*: refers to the ability of the latent space to cover all possible variations in the data. 
		- any point sampled from the latent space should correspond to a valid and meaningful data point when decoded
- if you want to restrict what the output should look like ensure a label is present $p(X,Y)$
- we use re-parameterisation as we cannot back-propagate due to it not being differentiable 
![[Screenshot 2025-10-13 at 12.41.05.png|400]]
![[Screenshot 2025-10-13 at 12.42.11.png|400]]
- the re-parameterisation trick allows tVAEs to be trained using standard gradient-based methods by transforming the sampling process into a differentiable function
- the re-perameterisation trick separates the stochastically of the sampling process from the determinising parts of the network
- the decoder is just sampling from the space created to generate the new data
![[Screenshot 2025-10-13 at 12.46.07.png|400]]
### Key Points
- VAEs compress data into abstract (latent) representations we can use to learn
- the reconstruction enables unsupervised learning
- re-parameterisation is a technique to train end-to-end
- pertubation ensures leans a smooth latent space
![[Screenshot 2025-10-13 at 12.47.40.png|400]]
- Hierarchical VAE is linked to the diffusion probabilistic model