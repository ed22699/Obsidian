---
tags:
  - Lesson
  - ensemble_methods
---
# Model selection
- select a model $h$ from a set of possible models in a set $H$
- the models in $H$ can differ in various ways, such as:
	- the structure of the model, e.g., differences in graphical models
	- the choice of prior distribution $p(\theta)$ over model parameters
	- the learning algorithm used e.g. EM, MCMC, backpropagation
	- parameters of the learning algorithm, like learning rate for stochastic gradient descent (SGD)
	- the features of the data used as inputs to the model 
	- the examples in the dataset the model is trained on
	- random initialisation of parameters for EM or SGD
## Hyperparameters
![[Screenshot 2024-11-04 at 09.11.14.png|300]]
- useful to characterise all of these modelling decisions as hyperparameters
- hyperparameters = all modelling choices that are fixed before training
## Model Selection on a Validation Set
- train a set of models $H$ with different hyperparameters
- choose the model $h$ that maximises performance on a validation set
	- can't tune on the training set as it would lead to overfitting
	- strengths:
		- optimises a performance metric we really care about
	- weaknesses:
		- didn't use all the data in training
		- if the validation set is small, we might choose the wrong model
- coming up with $H$
	- Random search: test random combinations of hyperparameters
	- Grid search: for each hyperparameter, define a set of values to test
		- use knowledge of problem to only test reasonable values
		- for numerical hyperparameters, e.g. learning rate, choose a aset of evenly-spaced values within a sensible range
		- $H$ contains all combinations of the chosen hyperparamter values
	- reduce the number of tests needed to find a good combination using a more intelligent strategy such as Bayesian Optimisation
### Cross-validation
![[Screenshot 2024-11-04 at 09.17.23.png|300]]
- split the training data into $k$ random, equally-sized subsets
- for each of the $k$ folds: leave out the $k^{th}$ subset from training, train on the rest and test on the $k^{th}$ subset
- compute the average performance across all $k$ folds
- avoids overfitting by tuning on training set performance
	- this is quite computationally expensive
- avoids tuning on a single small validation set
# Model Averaging
## Bayesian Model Averaging (BMA)
![[Bayesian Model Averaging (BMA)]]
# Ensembles
![[Ensembles]]
