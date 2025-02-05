---
tags:
  - multivariate_analysis
---
- standardise the data
- obtain the eigenvectors and eigenvalues from the covariance matrix or correlation matrix, or perform SVD
- sort eigenvalues (descending) and choose the $k$ eigenvectors that correspond to the $k$ largest eigenvalues ($k \leq n$)
- Construct the projection matrix $\textbf{R}$ from the selected $k$ eigenvectors
- Transform the original dataset $\textbf X$ via $\textbf R$ to obtain a $k$-dimensional feature subspace $\textbf P$