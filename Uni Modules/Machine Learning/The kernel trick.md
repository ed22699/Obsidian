---
tags:
  - kernal_support_vector
---
say the prediction for datapoint $\boldsymbol{x}$ is, for example $\boldsymbol{a}^T\Phi\phi(\boldsymbol{x})=\boldsymbol{a}^T\begin{pmatrix}k(\boldsymbol{x}_1,\boldsymbol{x})\\k(\boldsymbol{x}_2,\boldsymbol{x})\\k(\boldsymbol{x}_3,\boldsymbol{x})\end{pmatrix}$
- we just need the kernel function to make the prediction
- evaluate the kernel function values, e.g. $k(\boldsymbol{x}_1,\boldsymbol{x})$ without first computing $\phi(\boldsymbol{x}_1)$ and $\phi(\boldsymbol{x})$ and then computing their scalar product
- allows us to use very high-dimensional feature spaces since features are never directly computed