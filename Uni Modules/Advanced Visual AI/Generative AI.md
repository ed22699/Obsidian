---
tags:
  - Lesson
---
![[Screenshot 2025-10-13 at 12.06.59.png|500]]
## Generative Modelling
- *Concept*: what if we build a NN that can capture the distribution of the data
	- generative model takes as input training samples from a distribution and creates a model that represents that distribution
![[Screenshot 2025-10-13 at 12.09.44.png|400]]
- given a set of data instances $X$ and a set of labels $Y$
	- *Discriminative models*: discriminate between different kinds of data instances by capturing the *conditional* probability $p(Y|X)$
	- *Generative models*: can generate new data instances by capturing the *joint* probability $p(X,Y)$ or just $p(X)$ if there are no labels
		- examples of just $p(X)$
			- anomaly detection, such as detecting a tumour from medical images
			- style transfer, change the style of an image
			- deep fakes
			- inpainting
![[Screenshot 2025-10-13 at 12.15.29.png|400]]
## Autoencoders
- the encoder learns from data $x$ to create a low-dimensional latent space representation $z$ that captures the essential structure of the data
![[Screenshot 2025-10-13 at 12.17.01.png|200]]
- we reduce the layer dimensions so low level features are not captured, instead finds the deeper meaning, the useful information to generate it again
## Latent Space
- a space with learned abstract representations of the data where key features are stored
- it is a characteristic of generative models
- by manipulation the latent space new data can be generated that comply with the data patterns captured
- Example: In digit generation, each point in the latent space might represent a different digit structure (e.g., curvy or straight)  
- what it isn't
	-  Not every abstract or intermediate representation is latent space: 
		- It is not the final output layer of a neural network  
		- It is not the intermediate deep features, aka the representations of data at different layers  
		- It is not the model parameters (weights or biases)
![[Screenshot 2025-10-13 at 12.21.47.png|400]]
- autoencoders work well on denoising tasks
- problem with autoencoders is that the latent space may not be continuous or allow easy interpolation
	- solution: Variational Autoencoders
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
## Generative Adversarial Networks (GANs)
- if we can tell a model what looks real or fake during training, we can help it improve
	- human in the loop would be slow
	- create a model to determine whether the generation looks real
- designed with two models
	- a generator (G)
	- a discriminator (D)
	![[Screenshot 2025-10-15 at 09.05.21.png|400]]
- joint training: $\textbf G$ is generating samples from noise trying to fool $\textbf D$ and $\textbf D$ is trying to guess whether they are good enough
### Training
$$
\mathbb E _x [\log
$$
---
$$
\mathbb E _x [f(x)] \approx \frac 1 N \sum _1 ^N f(x_i)
$$
![[Screenshot 2025-10-15 at 09.09.17.png|300]]
#### Minimax Game
- train $\textbf D$ to maximise the probability of assigning the correct label to both training examples ($X_{real}$) and samples from $\textbf G$ ($X_{fake}$)
![[Screenshot 2025-10-15 at 09.12.01.png|400]]
---
- **there are also sigmoid and log graphs on this slide**
- train $\textbf G$ to minimise the second term so that $\textbf D$ classifies $G(z)$ as real
- **formula**
- global optimum: $\textbf G$ reproduces the true data distribution
#### Non-Saturating versioon



- generator might overfit towards certain images $\rightarrow$ add regularisation term


## Conditional Generative Adversarial Network (CGAN)
![[Screenshot 2025-10-15 at 09.23.59.png|300]]
![[Screenshot 2025-10-15 at 09.24.17.png|250]]
### Pix2Pix
- u-net is an encoder-decoder but with a skip connection
	- **look at U-net not in slides** 
- adding noise helps with robustness
	- also ensures more individual outputs that have slight differences
- we use the absolute error rather than MSE as it is more robust
	- MSE will change the network too much with outliers, such as if a pixel is slightly offset it will blow up the error
## Unpaired image-to-image translation
### CycleGAN
- background of zebra from horse example grass was more brown, this is because zebra lives in dryer grassland, this low level feature of the training images ultimately got passed through to the translation from horse to zebra
- used a lot in medical images
	- means you can use a low-dose CT scan that would include more noise and use a generator that is trained on high-dose CT scans to remove the noise
- can enhance video of low light using example of what images of the scene would look like in normal lighting
## CLIP (Contrastive Language-Image Pre-Training)
- conditioning with language
- CLIP learns to understand what an image means in natural language, not just to label it with a class name

1. Constructive Pre-training
![Discover How CLIP Bridges Text and Image Data|400](https://viso.ai/wp-content/uploads/2024/04/vision-language-models-clip-scaled.jpg)
![CLIP: Connecting text and images | OpenAI|400](https://images.ctfassets.net/kftzwdyauwt9/d9d46e4b-6d6a-4f9e-59a242ea1441/c7b386880f1af005fd02f159de7f4d00/overview-b.svg)