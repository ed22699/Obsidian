---
tags:
  - neural_networks
---
- in many ML methods its common to iteratively update the parameters by descending the gradient
![[Screenshot 2024-09-23 at 13.16.20.png|300]]
in neural network update the weights using:
- $w_{ji}=w_{ji}-\Delta w_{w_{ji}}$, where $\Delta w_{ji}=\sigma^{'}(y_{n}-t_{n})w_{kj}^{T}\sigma^{'}x_{i}$
- $w_{kj}=w_{kj}-\Delta w_{kj}$, where $\Delta w_{kj}= \sigma^{'}(y_{n}-t_{n})z_{j}$
- this is often done in mini-batches - using a small number of samples to compute $\Delta w$
