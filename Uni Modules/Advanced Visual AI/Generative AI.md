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
## Variational Autoencoders (VAEs)
![[Variational Autoencoders (VAEs)]]
## Generative Adversarial Networks (GANs)
![[Generative Adversarial Networks (GANs)]]
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