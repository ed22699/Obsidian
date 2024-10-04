---
tags:
  - kernal_support_vector
---

- gram matrix $\boldsymbol{K}$ is defined to be $\Phi\Phi^T$ 
- $K_{nm}=\phi(\boldsymbol{x}_n)^T\phi(\boldsymbol{x}_m)=k(\boldsymbol{x}_n, \boldsymbol{x}_m)$ is the similarity between the $n^{th}$ and $m^{th}$ datapoint
	- given data $\boldsymbol{x}_n$ and a particular choice of kernel $k$, we can computer the Gram matrix $\boldsymbol{K}$
- $\boldsymbol{K}$ is what we need for learning
>[!note]
$\boldsymbol{K}$ is symmetric