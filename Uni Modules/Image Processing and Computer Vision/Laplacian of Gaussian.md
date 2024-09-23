---
tags:
  - Filtering
---
- also known as LoG
- Laplacian is noise sensitive so it is always combined with a smoothing operation
![[Screenshot 2024-09-23 at 11.02.45.png|300]]
$$
\nabla^{2}(f(x,y)* G(x,y)) = \nabla^{2}G(x,y)*f(x,y)
$$
Laplacian of Gaussian-filtered image is equal to Laplacian of Gaussian filtered image