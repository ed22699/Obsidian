---
tags:
  - intro
---
- **Image Restoration**: recover an image that has been degraded by using a prior knowledge of the degradation phenomenon
	- Model the degradation and apply the inverse process to recover the original image
	![[Screenshot 2025-09-22 at 12.23.51.png|400]]
- if $H$ is a linear, position-invariant process, then the degraded image is given in the spatial domain by
$$
g(x,y) = h(x,y)* f(x,y)+ \eta(x,y)
$$
- in the frequency domain, the model becomes
$$
G(u,v) = H(u,v)F(u,v) +N(u,v)
$$
> [!NOTE]
> $\hat f (x,y)$ will never be precisely $f(x,y)$ but a good estimation

![[The Wiener filter]]

