---
tags:
  - multivariate_analysis
---
- t-SNE minimises divergence of two distributions over pairwise similarities of:
	- input objects ($P_i$)
	- corresponding low-dimensional points in the embedding ($Q_i$)
- student-t distribution rather than a Gaussian to compute the similarity between two points in the low-dimensional space
- assume a function that computes a distance between a pair of objects, e.g. Euclidean distance $d(x_i, x_j) = ||x_i =x_j||$ 
- minimise cost function (KL-divergence)
$$C = \sum _i KL(P_i||Q_i) = \sum _i \sum _j p_{j|i}\log p_{j|i}q_{j|i}$$
- t-SNE compares favourably to other techniques for data visualisation
- unclear how t-SNE performs on general dimensionality reduction tasks
- relatively local nature of t-SNE makes it sensitive to the curse of the intrinsic dimensionality of the data
- not guaranteed to converge to a global optimum of its cost function
![[Screenshot 2025-02-05 at 11.47.48.png|400]]