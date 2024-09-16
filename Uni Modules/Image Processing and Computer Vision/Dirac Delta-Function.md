---
tags:
  - Image_A_And_R
---

### Definition:
![[diracDefinition.png|150]]
$$
\int^{\infty}_{-\infty}\delta(t)dt = 1
$$
### Intuitively:
![[diracIntuative.png|150]]
$$
\delta(t) = \lim_{\in \to 0}[y_{\in}(t)]
$$
### Sifting Property:
$$
\int_{-\infty}^{\infty}f(t)\delta(t)dt = f(0) \to \int_{-\infty}^{\infty}f(t)\delta(t-\alpha)dt = f(\alpha)
$$
### Sampling in 2D to Obtain an Image
the sifting property can be used to express a 2D 'image function' as a linear combination of 2D Dirac pulses located at points (a, b) that cover the whole image plane
$$
\int_{-\infty}^{\infty}\int_{-\infty}^{\infty}f(a,b)\delta(a-x, b-y)da db = f(x,y)
$$