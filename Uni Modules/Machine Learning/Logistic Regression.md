---
tags:
  - Regression_and_Discriminant
  - neural_networks
---
- use logistic function to obtain the probability of class $C_{k}$: $y(\boldsymbol{x}) = \sigma(\boldsymbol{w}^{\boldsymbol{T}}\boldsymbol{x})$ where $\sigma$ denotes the logistic sigmoid function
![[Screenshot 2024-09-18 at 16.46.24.png|300]]
- s.t. when $y \to 0$ we choose class 2 and $y \to 1$ we choose class 1
	- $p(C_{1}|\boldsymbol{x}) = y(\boldsymbol{x})$ and $p(C_{2}|\boldsymbol{x}) = 1 - p(C_{1}|\boldsymbol{x})$ 
1. Define likelihood: For a dataset $\{x_{n}, t_{n}\}$, where the targets $t_{n} \in \{0,1\}$ we have $p(\boldsymbol{t}|\boldsymbol{x}, \boldsymbol{w}) = \Pi_{n=1}^{N}y_{n}^{t_{n}}(1-y_{n})^{1-t_{n}}$ where $y_{n} = p(C_{1}|x_{n})$
2. Take negative logarithm of the likelihood
$$
		-\ln p(\boldsymbol{t}|\boldsymbol{x}, \boldsymbol{w}) = -\sum_{n=1}^{N}\{t_{n}\ln y_{n} + (1 - t_{n})\ln (1 - y_{n})\}
$$
3. Calculate the derivative w.r.t. the parameters $\boldsymbol{w}$:
$$
\frac{d \ln p(\boldsymbol{t}|\boldsymbol{x}, \boldsymbol{w})}{d \boldsymbol{w}} = \sum_{n=1}^{N}(y_{n}-t_{n})x_{n}
$$
4. Now use Eq. above to directly update $\boldsymbol{w}$ using the data $x$

## MLE using Gradient Descent
![[Screenshot 2024-09-18 at 17.08.33.png|400]]
- start with random weight values
- adjust each weight $w$ to minimise negative log likelihood (move downhill to a minimum)
- the derivative represents the slope $\frac{d \ln p(\boldsymbol{t}|\boldsymbol{x}, \boldsymbol{w})}{d \boldsymbol{w}} = \sum_{n=1}^{N}(y_{n}-t_{n})x_{n}$
- increase of decrease $w$ by a small amount in the downward direction
- in case of logistic regression the error function is convex which means it has a unique minimum