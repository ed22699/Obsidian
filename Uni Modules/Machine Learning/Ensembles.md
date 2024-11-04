---
tags:
  - ensemble_methods
---
- Ensemble: a combination of different models
	- goes off the concept of the wisdom of the crowd (the combination of predictions is more effective than any one 'model')
	- often outperforms the average individual, and sometimes even the best individual
- different to [[Bayesian Model Averaging (BMA)]]
	- BMA weights try to identify a singe, correct model
	- BMA weights do not provide the optimal combination
## Expected Error
Given a set of models, $1, ..., M$
- $y_m(x)$ is the prediction from model m.
- Simple ensemble: the mean of the individual predictions, $y_{COM} =\frac 1 M \sum^M _{m=1} y_m(x)$
- if you compare the sum-of-squares error of $y_{COM}$ with that of the individual models
	- error of our combination for a particular input $\boldsymbol x$ is: $(y(\boldsymbol x)-y_{COM}(\boldsymbol x))^2=(\frac 1M\sum_{m=1}^M(y(\boldsymbol x)-y_m(\boldsymbol x)))^2$
	- expected error of our combination is $E_{COM}=\mathbb{E}_x[(y(\boldsymbol x)-y_{COM}(\boldsymbol x))^2]=\mathbb E_x[(\frac 1M\sum_{m=1}^M(y(\boldsymbol x)-y_m(\boldsymbol x)))^2]$
	- expected error of an individual model $m$ is: $E_m=\mathbb{E}_x[(y(\boldsymbol x)-y_m(\boldsymbol x))^2]$
	