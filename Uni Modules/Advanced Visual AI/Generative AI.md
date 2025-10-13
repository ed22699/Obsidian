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
![[Screenshot 2025-10-13 at 12.22.08.png|400]]
![[Screenshot 2025-10-13 at 12.22.55.png|400]]