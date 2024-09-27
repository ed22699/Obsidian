---
tags:
  - freq_domain_and_trans
---
**transforms a signal sampled in time or space to the same signal sampled in temporal or spatial frequency**
## Continuous Form
- of two variables $f(x,y)$ is:
$$
F(u,v)=\int_{-\infty}^{\infty}\int_{-\infty}^{\infty}f(x,y)e^{-i2\pi(ux+vx)}dxdy
$$
- conversely, given $F(u,v)$ we can obtain $f(x,y)$ by means of inverse Fourier Transform
$$
f(x,y)=\int_{-\infty}^{\infty}\int_{-\infty}^{\infty}F(u,v)e^{i2\pi(ux+vy)}dudv
$$
- also known as the Fourier Transform pair
- constitute a lossless representation of data
# Discrete Form
- of two variables $f(x,y)$ is:
$$
F(u,v)=\frac{1}{N^{2}}\sum_{x=0}^{N-1}\sum_{y=0}^{N-1}f(x,y)e^{-i2\pi(\frac{ux+vy}{N})}
$$
for $u,v = 0,1,2,...,N-1$
- conversely, given $F(u,v)$ we can obtain $f(x,y)$ by means of inverse FT
$$
f(x,y) = \sum_{u=0}^{N-1}\sum_{v=0}^{N-1}F(u,v)e^{i2\pi(\frac{ux+vy}{N})}
$$
for $x,y = 0,1,2,...,N-1$

- Euler's formula: $e^{i\theta}= \cos \theta + i \sin \theta$
- each term of the Fourier Transform is composed of the sum of all values of the image function $f(x,y)$ multiplied by a particular kernel at a particular frequency and orientation specified by $(u,v)$
$$
F(u,v)=\frac{1}{N^{2}}\sum_{x=0}^{N-1}\sum_{y=0}^{N-1}f(x,y)[\cos(\frac{2\pi(ux+vy)}{N})-i\sin(\frac{2\pi(ux+vy)}{N})]
$$
for $u,v=0,1,2,...,N-1$
- the slowest varying frequency component, i.e. when $u=0,v=0\to$ average image graylevel 
- all kernels together form a new orthogonal basis for our images
![[Screenshot 2024-09-25 at 10.47.54.png|400]]
![[Screenshot 2024-09-27 at 07.50.08.png|200]]
- ideal edge and line structures have a concentration along a line passing though the origin in the frequency domain in a direction perpendicular to their orientation
- constructed by adding together all 2D sinusoidal waves that travel perpendicular to the edge or line
![[Screenshot 2024-09-27 at 07.50.56.png|300]]
![[Screenshot 2024-09-27 at 07.54.50.png|400]]
>[!hint]
 each dot on the FT space represents a $u$ and $v$ value, hence many of these dots with varying positions will form a grayscaled image

 