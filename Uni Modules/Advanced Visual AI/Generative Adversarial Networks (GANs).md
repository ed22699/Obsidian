---
tags:
  - generative_ai
---
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
\mathbb E _x [\log(D(x))] +\mathbb E_z [\log(1-D(G(z)))]
$$
$$
\mathbb E _x [f(x)] \approx \frac 1 N \sum _1 ^N f(x_i)
$$
![[Screenshot 2025-10-15 at 09.09.17.png|300]]
#### Minimax Game
- train $\textbf D$ to maximise the probability of assigning the correct label to both training examples ($X_{real}$) and samples from $\textbf G$ ($X_{fake}$)
	- assign high scores to real data and low scores to fake data
![[Screenshot 2025-10-15 at 09.12.01.png|400]]
- train $\textbf G$ to minimise the second term so that $\textbf D$ classifies $G(z)$ as real
![[Screenshot 2025-10-15 at 15.09.24.png|300]]
- global optimum: $\textbf G$ reproduces the true data distribution
#### Non-Saturating version
- train $\textbf G$: in early learning, $\log(1-D(G(z)))$ may saturate
$$
\max_G \mathbb E_z[\log (D(G(z)))]
$$
- this version avoids vanishing gradients when $\textbf D$ is too strong 
### Training Challenges
- Mode collapse:
	- the generator can only generate one type of image, i.e. your GAN trained on real life images can only generate images of dogs
	- the discriminator things they're like-like, therefore no further exploration will take place
	- losses to try and increase diversity have been proposed
![[Screenshot 2025-10-15 at 15.16.09.png|300]]
- Convergence failure:
	- it fails to find an equilibrium between the Generator and the Discriminator 
	- one model training quicker than the other is the most common case
![[Screenshot 2025-10-15 at 15.15.45.png|300]]
- *solutions for improved training*
	- (Euclidean) loss between generated images and example image: $L_{L2}=\frac 1 N \sum _{i=1}^N ||G(z)_i - x_i||_2^2$
	- generator might overfit towards certain images $\rightarrow$ add regularisation term
	- better hyperparameter selections
	- leaky ReLU for the Discriminator
	- Batch Normalisation
	- Increase Stride of Convolution in Discriminator
	- Scheduling Generator and Discriminator training to be balanced
### After Training GANs
#### generating new data
![[Screenshot 2025-10-15 at 15.19.43.png|300]]
- we just need to go back to the $G$ model and generate new instances
- GANs are distribution transformers
- you can traverse/interpolate within this data distribution and produce different images
- apply perturbation to generate similar images across the target distribution

