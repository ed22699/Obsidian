---
tags:
  - ensemble_methods
---
- model selection does not always pick out one model, $h$, as a clear winner
- we may be uncertain about which model is correct
	- so we express uncertainty by assigning a probability to each model given the training data, $p(h|\boldsymbol{X})$
- rather than choosing a single model, we can take an expectation
- predictions now come from a weighted sum over models, where $p(h|\boldsymbol{X})$ are weights:
	$$
	p(z|\boldsymbol{X})=\sum_{h=1}^Hp(z|\boldsymbol{X}, h)p(h|\boldsymbol X)
	$$
	- apply Bayes' rule to estimate the weights: $p(h|\boldsymbol X)=\frac{p(\boldsymbol X|h)p(h)}{\sum_{h'=1}^H p(\boldsymbol X|h')p(h')}$
	- when we increase the amount of data in $\boldsymbol X$:
		- $p(h|\boldsymbol X)$ becomes more focussed on one model
		- so BMA is soft model selection, it does not combine models to make a more powerful model