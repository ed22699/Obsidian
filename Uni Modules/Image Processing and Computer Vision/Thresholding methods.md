---
tags:
  - segmentation
---
- pixels are categorised based on intensity
- only useful when sufficient contrast exists
Perfect segmentation is difficult to achieve:
- pixel may straddle the "real" boundary of objects such that it partially belongs to two or more objects
- effects of noise, non-uniform illumination, occlusions etc. give rise to the problem of [[Over-segmentation]] and [[Under-segmentation]]
## Method
- if the image contains a dark object on a light background
	- choose a threshold value, $T$
	- for each pixel, if the brightness at that pixel is less than $T$, it is a pixel of interest, else it is part of the background
- threshold value is important
	- too high $\to$ background pixels classified as foreground
	- too low $\to$ foreground pixels classified as background
![[Screenshot 2024-10-01 at 11.58.43.png|100]]
### choosing a threshold value
- use the image histogram
	- count how many pixels in the image have each value
	- for simple images it shows peaks and alleys around regions of the image
	![[Screenshot 2024-10-01 at 12.01.26.png|100]]
- ![[threshold selection algorithm]]
## Issues
issues occur when working with image types that are
- dark
- light
- low contrast
- high contrast