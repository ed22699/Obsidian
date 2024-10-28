---
tags:
  - sequential_data
---
- A state space model
- $\boldsymbol{z}_n$ are latent (unobserved) discrete state variables
- $\boldsymbol{x}_n$ are observations, which may be discrete or continuous values depending on the application
![[Screenshot 2024-10-28 at 10.44.57.png|150]]
### Sequence Labelling for Text
- sequence labelling: classifying data points in a sequence
	- e.g. classifying words in a text document into grammatical categories such as noun, verb, adjective, etc
	- this is called part-of-speech (POS) tagging and is used by natural language understanding systems e.g. to extract facts and events from text data
	![[Screenshot 2024-10-28 at 10.49.56.png|200]]
- we use an HMM model for human action recognition as actions typically follow a temporal sequence
- HMMs can be used for different goals:
	- inferring the latent states (sequence labelling)
	- predicting the next latent state
	- predicting the next observation
- HMMs can be used with different levels of supervision:
	- **Supervised**: latent states are given in the training set
	- **Unsupervised**: no labels for the latent states, so the model seeks an assignment that best explains the observations given the model 
	- **Semi-supervised**: some labels are given, but the model is learned over both labelled and unlabelled data
		- avoids overfitting to a very small labelled dataset while identifying latent states that follow the desired labelling scheme
- the probabilistic model of the HMM is made up of two main parts:
	- **The transition distribution**: can be represented as a transition matrix and models the dependencies between the latent states
		- probability of $\boldsymbol{z}_n$ depends on the previous state: $p(\boldsymbol{z}_n|\boldsymbol{z}_{n-1})$
		- given $K$ labels (state values), we can write all the values of $p(\boldsymbol{z}_n=k|\boldsymbol{z}_{n-1=l})$ in a transition matrix, $\boldsymbol{A}$
			- rows correspond to values of the previous state, $\boldsymbol{z}_{n-1}$
			- columns are values of the current state, $\boldsymbol{z}_n$
			![[Screenshot 2024-10-28 at 11.03.12.png|200]]
		- a vector of probabilities $\pi$ is used for $\boldsymbol{z_1}$ (to give the initial state probabilities), this us does to it having no predecessor
		- a transition matrix for a mixture model would have all rows looking the same as data is independent
	- **The emission distributions**: models the observations given each latent state value
		- distribution over the observed variables, $p(\boldsymbol{x}_n|\boldsymbol{z}_n, \phi)$, where $\phi$ are paramets of the distributions, e.g.
			- 



english language makes sequential text difficult as it has a lot of ambiguity when it comes to nouns, verbs, etc

[[EM algorithm]]