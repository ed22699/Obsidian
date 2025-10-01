---
tags:
  - Lesson
---
## Laplace Prior - soft thresholding
- assume that the likelihood function is
$$
p(x|\theta) = \frac 1 {\sigma _n \sqrt{2\pi}} \exp -\frac{(x-\theta)^2}{2\sigma ^2_n}
$$
- prior pdf is
$$
p(\theta) = \frac{1}{\sigma \sqrt{2}}\exp - \frac{\sqrt 2 |\theta|}{\sigma}
$$
- using the [[The Maximum a Posteriori (MAP) Estimator]] we can get 
$$
\hat \theta = x - \sqrt 2 \frac{\sigma _n ^2 }{\sigma}sign(\theta)
$$
or 
$$
\hat \theta = sign(x)(|x| - \sqrt 2 \frac {\sigma _n ^2}{\sigma})_+, \; where (g)_+ = \begin{cases}
0, & g < 0 \\ g, & otherwise
\end{cases}
$$
![[Screenshot 2025-09-29 at 15.06.32.png|500]]
## Deep Image Prior (DIP)
![[Deep Image Prior (DIP)]]

