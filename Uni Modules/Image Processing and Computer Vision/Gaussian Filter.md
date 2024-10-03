---
tags:
  - Filtering
---

- used for smoothing
- parameter $\sigma$ determines the width of the filter and hence the amount of smoothing (higher $\sigma$ means more blurred)
	- 1D: $g(x) = \frac{1}{\sqrt{2\pi} \sigma}e^{-\frac{x^{2}}{2\sigma ^{2}}}$
	![[Screenshot 2024-09-23 at 10.04.29.png|150]]
	- 2D: $g(x,y) = \frac{1}{2\pi \sigma}e^{-\frac{x^{2}+y^{2}}{2\sigma ^{2}}}$
	![[Screenshot 2024-09-23 at 10.05.02.png|300]]	
- 2D Gaussian can be achieved faster using two 1D Gaussian filters as linear Gaussian kernel is separable
	$$
	K = \frac{1}{256}\begin{pmatrix}1&4&6&4&1\\4&16&24&16&4\\6&24&36&24&6\\4&16&24&16&4\\1&4&6&4&1\end{pmatrix}=\frac{1}{16}\begin{pmatrix}1\\4\\6\\4\\1\end{pmatrix}\cdot\frac{1}{16}\begin{pmatrix}1&4&6&4&1\end{pmatrix}
	$$
	$$
	g(x,y) = \frac{1}{2\pi \sigma}e^{-\frac{x^{2}+y^{2}}{2\sigma ^{2}}} = (\frac{1}{2\pi \sigma}e^{-\frac{x^{2}}{2\sigma ^{2}}})(\frac{1}{2\pi \sigma}e^{-\frac{y^{2}}{2\sigma ^{2}}})=g(x)g(y)
	$$
	- filtering an $m$ x $m$ image with an $n$ x $n$ kernel is $O(m^{2}n^{2})$ complexity, but with a separable kernel it is $O(m^{2}n)$ which is a significant reduction
- smoothing an image makes it easier for the net stage of processing e.g. edge detection (due to noise reduction)