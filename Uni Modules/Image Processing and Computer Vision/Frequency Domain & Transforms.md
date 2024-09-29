---
tags:
  - Lesson
  - freq_domain_and_trans
---
# Signals as Functions
frequency - allows us to characterise signals
- repeats over regular intervals with frequency $u=\frac{1}{T}$ cycles/sec (Hz)
- amplitude $a$ (peak value)
- the phase $\theta$ (shift in degrees)
![[Fourier's Theorem]]


![[2D Fourier Transform]]
# Frequency Domain
- $F(u,v)$ is a complex number and has real and imaginary parts: $F(u,v)= R(u,v)+iI(u,v)$ 
- Magnitudes (forming the magnitude spectrum): $|F(u,v)|=\sqrt{R^{2}(u,v)+I^{2}(u,v)}$ 
- Phase angles (forming the phase spectrum): $\theta(u,v)= \tan^{-1}[I(u,v)/R(u,v)]$
- Expressing $F(u,v)$ in polar coordinates $(r, \theta)$: $F(u,v)= |F(u,v)|e^{i\theta (u,v)}= re^{i\theta}$
![[Screenshot 2024-09-25 at 10.52.44.png|400]]
- Power Spectrum: $|F(u,v)| = \sqrt{R^{2}(u,v)+I^{2}(u,v)}$
![[Screenshot 2024-09-25 at 10.53.09.png|200]]
- Phase Spectrum: $\theta(u,v)=\tan^{-1}[I(u,v)/R(u,v)]$ 
![[Screenshot 2024-09-25 at 10.53.49.png|200]]
## Fourier spaces and their inverse transforms back
Spaces:
![[Screenshot 2024-09-27 at 08.05.01.png|300]]
Inverse Transform back to image space
![[Screenshot 2024-09-27 at 08.05.19.png|300]]
>[!note]
 higher frequencies represent the finer details of an image, hence you will get a 'blurry' image by removing these higher frequencies (due to the magnitudes of these frequencies being smaller)
- you can manipulate the FS to alter image qualities, e.g.
![[Screenshot 2024-09-27 at 08.08.17.png|500]]
## Separability of FT
- if 2D transform is separable, the result can be found by successive application of two 1D transformations (principle aspect of the Fast Fourier Transform)
### Convolution theorem
- convolution in spatial domain is equivalent to multiplication in frequency domain (and vice versa)
	- $h=f*g$ implies $H=FG$
	- $h=fg$ implies $H=F*G$
	![[Filters in FS]]
- Translation/shift in spatial domain:
	- result in a linear phase change in the frequency domain, but no change in the magnitude spectrum, hence it looks the same wherever it is in the image
- Rotation in spatial domain:
	- rotation in spatial domain results in a corresponding rotation in the Fourier domain
## Using D instead of r
- Lowpass filters, $D_{0}$ is the cutoff frequency and $n$ is the order of the Butterworth filter
![[Screenshot 2024-09-27 at 18.03.59.png|500]]
- Highpass filters, $D_{0}$ is the cutoff frequency and $n$ is the order of the Butterworth filter
![[Screenshot 2024-09-27 at 18.05.10.png|500]]
