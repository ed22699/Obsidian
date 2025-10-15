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
![[Screenshot 2025-10-15 at 09.12.01.png|400]]
- assign high scores to real data and low scores to fake data
- train $\textbf G$ to minimise the second term so that $\textbf D$ classifies $G(z)$ as real
- **formula**
- global optimum: $\textbf G$ reproduces the true data distribution
#### Non-Saturating versioon



- generator might overfit towards certain images $\rightarrow$ add regularisation term

