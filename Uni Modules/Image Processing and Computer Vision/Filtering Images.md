---
tags:
  - Lesson
  - Filtering
---
# Image Transforms
- converts an image into a new representation of the input data
- transformations are used in filtering, compression, feature extraction etc
- filer = kernel = mask (same thing)
# Convolution
- mathematical operation on two functions ($f$ and $g$) that produces a third function ($h=f*g$), representing how the shape of one is modified by the other
$$
f * g = \int_{-\infty}^{\infty}f(x-t)g(x) dt
$$
- use for filtering images in the spatial domain
- application in other parameter spaces, e.g. frequency domain
- fundamental to convolutional neural nets for deep learning
- main aim of convolution is understanding how a system or signal responds to an input, used for applying filters
## 1D discrete convolution
$g(x)=h(x)*f(x)$ 
- $f$ is the signal, $h$ is the convolution filter ($h$ has an origin and a normalisation factor)
- defined as $g(x) = \sum_{m=-s}^{s}f(x-m)h(m)$ for $s \geq 1$ 
![[Screenshot 2024-09-22 at 09.05.18.png|200]]
## 2D discrete convolution
$$
g(x,y)=\sum_{m}\sum_{n}f(x-m, y-n)h(m,n)
$$
![[Screenshot 2024-09-22 at 09.07.04.png|400]]
## 2D discrete correlation
$$
g(x,y)=\sum_{m}\sum_{n}f(x+m, y+n)h(m,n)
$$
- correlation measures the similarity between two signals or datasets, used for matching patterns
- correlation $\equiv$ convolution when kernel is symmetric under $180^{\circ}$ rotation, e.g. $\begin{bmatrix}a&b&c\\d&e&d\\c&b&a\end{bmatrix}$ 
## Convolution properties
- commutative: $f*h=h*f$
- associative: $(f*g)*h=f*(g*h)$
- distributes over addition: $f*(g+h)=(f*g) + (f*h)$ (useful for simplifying high computational equations)
- scalars factor out: $af*g=f*ag=a(f*g)$
- identity: given unit impulse $e=[...,0,0,1,0,0,...]$ then $f*e=f$
![[Screenshot 2024-09-22 at 09.32.09.png|400]]
## Normalising the convolution result
- weights will affect pixel values, normalise them such that they sum to 1
	- smooth: $\frac{1}{9}\begin{bmatrix}1&1&1\\1&1&1\\1&1&1\end{bmatrix}$
	- 3x3 gaussian blur: $\frac{1}{16}\begin{bmatrix}1&2&1\\2&4&2\\1&2&1\end{bmatrix}$
	- sharpen: $\begin{bmatrix}0&-1&0\\-1&4&-1\\0&-1&0\end{bmatrix}$
	- basic edge detector: $\begin{bmatrix}-1&-1&-1\\-1&8&-1\\-1&-1&-1\end{bmatrix}$
![[Gaussian Filter]]
![[Median Filter]]
# Sharpening
- sharpening spatial filters seek to highlight fine detail
	- remove blurring from images
	- highlight edges
- 