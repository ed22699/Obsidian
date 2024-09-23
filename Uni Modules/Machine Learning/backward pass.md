---
tags:
  - neural_networks
---
- optimise weights using derivatives to find a solution, back-propagating the output error signal across the network
 ![[Screenshot 2024-09-23 at 12.00.58.png|300]]
- this image is a special case where the output layer has a single node. In the general case we could have e.g. $E=\sum_{k}(y_{k}-t_{k})^{2}$
	- error for entire dataset breaks down into a sum of errors for each individual datapoint: $E(\boldsymbol{w})=\sum_{n=1}^{N}E_{n}(\boldsymbol{w})$
	- this means error gradient for the entire dataset with respect to some weight $w_{ji}$ will just be the sum of error gradients for each datapoint: $\frac{dE}{dw_{ji}}=\sum_{n=1}^{N}\frac{dE_{n}}{dw_{ji}}$
	- focus on computing the $\frac{dE_{n}}{dw_{ji}}$ values 
## Computing partial derivatives
- consider an arbitrary unit $j$ (aka 'node') in a neural network
- associate the bias for a unit with a dummy input fixed to $1$ 
- unit computes a value $z_{j}$ by first computing $a_{j}$, a weighted sum of its inputs (from previous layer), and then sending $a_{j}$ to some **nonlinear** activation function $h$ 
$$
a_{j} = \sum_{i}w_{ji}z_{i}
\tag{1}
$$
$$
z_{j} = h(a_{j})
\tag{2}
$$
- since $E_{n}$ only depends on the weight $w_{ji}$ via $a_{j}$ we can write
$$
\frac{dE_{n}}{dw_{ji}} = \frac{dE_{n}}{da_{j}}\frac{da_{j}}{dw_{ji}}
\tag{3}
$$
- since $a_{j}=\sum_{i}w_{ji}z_{i}$
$$
\frac{da_{j}}{dw_{ji}} = z_{i}
$$
- if we introduce some notation $\delta_{j} \equiv \frac{dE_{n}}{da_{j}}$ 
$$
\frac{dE_{n}}{dw}
\tag{4}$$