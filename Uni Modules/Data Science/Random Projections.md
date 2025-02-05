---
tags:
  - multivariate_analysis
---
- $\textbf P = \textbf X \textbf R$
- where:
	- $\textbf X \in \mathcal R ^{m \times n}$ (data matrix)
	- $\textbf R \in \mathcal R ^{k \times m}$ (projection matrix)
	- $\textbf P \in \mathcal R ^{m \times k}$ (lower dimensional representation)
### Gaussian Random Projections
- first row is a random unit vector uniformly chosen from $S^{n-1}$
- second row is a r.u.v. from the space orthogonal to the first row
- third row is a r.u.v. from the space orthogonal to the first two rows, etc
- in this way of choosing $\textbf R$, the following properties are satisfied:
	- spherical symmetry: for $\textbf A \in O(n)$, i.e. $\textbf A \textbf A ^T = \textbf A ^T \textbf A = \textbf I$, $\textbf A \textbf R$ and $\textbf R$ have the same distribution
	- orthogonality: the rows of $\textbf R$ are orthogonal to each other
	- normality: the rows of $\textbf R$ are unit-length vectors
#### Johnson-Lindenstrauss Lemma
- Given $0 < \epsilon < 1$, a set $X$ of $m$ points is $\mathcal{R}^n$, and a number $k > 8 \frac {\log (m)}{\epsilon ^2}$, there is a linear map $f:\mathcal R ^n \rightarrow \mathcal R ^k$ such that:
	$$(1-\epsilon)||u-v||^2 \leq ||f(u) - f(v)||^2 \leq (1+\epsilon)||u-v||^2$$
	- for all $u, v \in X$
- an orthogonal projection will, in general, reduce the average distance between points
- compatible with approximate nearest neighbours
### Database friendly random projections
![[Screenshot 2025-02-05 at 11.37.34.png|200]]
