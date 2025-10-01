---
tags:
  - optimisation
---

- *idea*: smooth RMSprop's usually 'noisy' incoming gradient using a new parameter $\alpha$
$$
G_{t+1}=\alpha G_t + (1-\alpha)\nabla J (X;W_t)
$$
$$
A_{t+1} = \beta A_t + (1-\beta)(\nabla J (X;W_t))^2
$$
$$
W_{t+1} = W_t - \eta \frac{G_{t+1}}{(\sqrt A_{t+1} + \varepsilon)}
$$
- *idea*: correct for the impact of bias introduced by 'initialising' the two smoothed measures
	- i.e. starting with $t=1$ 'fade-in' the smoothing effect exponentially by introducing $\bar G$ and $\bar A$
$$
G_{t+1}=\alpha G_t + (1-\alpha)\nabla J (X;W_t)
$$
$$
\bar G = G_{t+1}/(1-\alpha ^t)
$$
$$
A_{t+1} = \beta A_t + (1-\beta)(\nabla J (X;W_t))^2
$$
$$
\bar A + A_{t+1} / (1-\beta ^t)
$$
$$
W_{t+1} = W_t - \eta \frac{\bar G}{(\sqrt {\bar A } + \varepsilon)}
$$
![[Screenshot 2025-10-01 at 17.52.24.png|500]]