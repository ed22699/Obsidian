---
tags:
  - neural_networks
---
1. Calculate activations of the hidden layer $h$: $a_{j}=\sum_{i=1}^{D}w_{ji}^{(h)}x_{i}+w_{j0}^{(h)}$ (this is linear)
2. Pass it through a nonlinear function: $z_{j}=\sigma(a_{j})$ (in MLP typically use sigmoid functions)
3. Calculate activations of the output layer $o$: $a_{k}=\sum_{j=1}^{hiddensize}w_{kj}^{(o)}z_{j}+w_{k0}^{(o)}$
4. Compute predictions using a sigmoid: $y_{k}=\sigma(a_{k})$ (nonlinear)

Summary:
$$
y_{k}=\sigma(\sum_{i=1}^{D}w_{kj}\sigma(\sum_{i=1}^{D}w_{ji}x_{i}^{(h)}+w_{j0}^{(h)})+w_{k0}^{(o)})
$$

