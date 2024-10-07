---
tags:
  - Lesson
  - probabilistic_graphical_models
---
**Chain Rule**: $P(x_1,...x_n)=P(x_1)P(x_2|x_1)...P(x_n|x_1,...,x_{n-1})$
- with conditional independence: $P(x_3|x_1,x_2)=P(x_3|x_2)$
	- distribution $P$, $x_3$ is independent of $x_1$ conditional on $x_2$
	- so $P(x_1,...,x_n)=P