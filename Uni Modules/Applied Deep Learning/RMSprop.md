---
tags:
  - optimisation
---

- *idea*: root-mean-square propagation 
	- combat the aggressive reduction in Adagrad's learning speed by propagation of a smooth running average
- update equations now introduce a smoothing parameter $\beta$:
$$
A_{t+1} = \beta A_t + (1-\beta)(\nabla J (X;W_t))^2
$$
$$
W_{t+1} = W_t - \eta \frac{\nabla J (X; W_t)}{(\sqrt A_{t+1} + \varepsilon)}
$$
- RMSprop you can think of $\beta$ as a forgetful parameter, as time goes on it remembers less of the previous 
- just adding standard momentum does not help much in improving performance further
	- further smoothing and correction operations can be applied
![[Screenshot 2025-10-01 at 17.39.44.png|500]]