---
tags:
  - intro
---
- Hit-or-miss cost function
$$
C(\varepsilon) = \begin{cases}
0, |\theta - \hat \theta| < \delta \\
1, otherwise
\end{cases}
$$
- General Bayesian estimator
$$
\hat \theta(x) = \arg _\theta \min \int C[\theta, \hat \theta (x)]p(\theta | x)d\theta
$$
- Using the above equations, the MAP is obtained as
$$
\hat \theta (x) = \arg _\theta \min \int _{|\theta - \hat \theta| \geq \delta} p(\theta|x)d\theta
$$
- or can also be written as
$$
\hat \theta (x) = \arg _\theta \min [1- \int_{|\theta - \hat \theta| < \delta} p(\theta|x)d\theta
$$
- To minimise the expected cost, when $\delta \rightarrow 0$ one should select the MAP equation, that is, the mode of the posterior pdf
$$
\hat \theta (x) = \arg _\theta \max p(\theta |x)
$$
- Using Bayes theorem together with the last equation, we can also write the MAP equation as below (more useful in practice)
$$
\hat \theta (x) = \arg _\theta \max p(x|\theta) p(\theta)
$$
$$
\hat \theta (x) = \arg _\theta \max [\ln p(x|\theta) + \ln p(\theta)]
$$
![[Screenshot 2025-09-22 at 15.21.48.png|400]]
![[Screenshot 2025-09-22 at 15.22.59.png|400]]
