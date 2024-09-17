---
tags:
  - Lesson
  - MLConcepts
---
# Forms of machine learning
- attempts to learn models of the world
- data defines possible form of learning
## [[Unsupervised Learning]] 
## [[Supervised Learning]]
## [[Reinforcement Learning]] (Not Taught in Unit)
# Underfitting VS Overfitting
- Underfitting: A model that is too simple
- Overfitting: A model that fits minor variations or noise
## Model Selection
- Common method is to split the dataset (use half to fit, half to test)
	- Training dataset: Used for training/optimising your model
	- Validation dataset: Used only for validating your model
### Problems
- Relying only on validation dataset to select our models can lead us to overfit to that data, in particular for small datasets and iterative methods. To solve this we use a third subset:
	- Testing dataset: Used to test the model for general fitting quality after the optimisation procedure has finished
- we end up with less data for training the model. cycle over multiple subsets fo the data using cross-validation
	- Cross-validation: original data is split into S groups so that (S-1)/S data is used for training
	- common to set S to a relatively low number, e.g. S = 4
	- White blocks = training, red blocks = validation
	 ![[modelSelection.png|200]]
# [[Curse of Dimensionality in ML]]	
# [[No Free Lunch Theorem]]
# Parametric VS Non-Parametric Models	
- Parametric: Model assumes a fixed number of parameters
	- Pros: Simpler, fast to fit and may require less data
	- Cons: Complexity is fixed. Simple models are better for simpler problems/datasets
- Non-parametric: Number of model parameters grows with the amount of data
	- Pros: Flexible (infer which functions to use), weak assumptions, can give better models
	- Cons: More expensive to train (especially with large datasets as more parameters), risk of overfitting
# Reading
- Bishop 1.1-1.4
[[Bishop 1.1]]