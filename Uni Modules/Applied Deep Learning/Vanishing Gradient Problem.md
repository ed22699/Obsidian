---
tags:
  - backpropagation
---
- the further we propagate the error derivative backwards (e.g. $l$ being small), the more often we multiply $\delta$ with a very small number $\tanh' < 1$, potentially making learning extremely slow or suppress it completely in early layers
$$
\delta_i ^{l-1} = g_i^{'l-1} \sum_{j=1}^{d(l)}w_{ij}^l \delta _j ^l = \underbrace{g_i^{'l-1}\sum_{j=1}^{d(l)} w_{ij}^l (g_j^{'l} \sum_{k=1}^{d(l+1)}w_{jk}^{l+1}(...))}_{g' \; appears \; (N-l+1) \; times \; as \; factor}
$$
![[Screenshot 2025-09-27 at 13.08.09.png|400]]
- problem: $\tanh$ becomes close to 0 when 'saturated' 
	- this causes early layers in particular to learn much slower if at all (since the gradient may vanish exponentially)
- helpful measures
	- hierarchical pre-training of shallow networks
	- extensively slow+ling training on all data helps
	- propagate alternatives to gradient (e.g. sign of gradient)
	- forward signal via residual neural networks (ResNet)
	- other, specially robust neuron layouts