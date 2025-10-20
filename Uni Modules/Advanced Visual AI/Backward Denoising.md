---
tags:
  - generative_ai_diffusion
---
- *backward* or reverse denoising process that learns to generate data by denoising
![[Screenshot 2025-10-20 at 12.39.12.png|400]]
![[Screenshot 2025-10-20 at 12.42.41.png|500]]
- we do not know what the true posterior is so we use a NN parameterised with $\theta$ to approximate the true posterior
$$
p_\theta (x_{t-1}|x_t) \approx q(x_{t-1}|x_t, x_0)
$$
![[Screenshot 2025-10-20 at 12.49.26.png|500]]
- if for any step $t$, NN $\theta$ can always predict the injected noise, then by removing the noise step by step, we will get a clean image
- each reverse process, we sample a different $x_T\sim \mathcal N(0,I)$ so generate a different new image
![[Screenshot 2025-10-20 at 12.51.30.png|400]]
![[Screenshot 2025-10-20 at 12.52.41.png|500]]