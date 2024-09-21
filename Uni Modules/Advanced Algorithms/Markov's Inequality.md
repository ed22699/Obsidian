---
tags:
  - probability
  - Hashing
---
if $X$ is a non-negative r.v., then for all $a > 0$ 
$$
P(X \geq a)\leq \frac{\mathbb{E}(X)}{a}
$$
## Example
- suppose the that average speed on the motorway is $60mph$ 
- $P($speed of a random car $\geq 120mph) \leq \frac{60}{120} = \frac{1}{2}$
- $P($speed of a random car $\geq 90mph) \leq \frac{60}{90} = \frac{2}{3}$

>[!abstract] Corollary
>if $X$ is a non-negative r.v. that only takes **integer** values, then
>$P(X >0)=P(X \geq 1) \leq \mathbb{E}(X)$

