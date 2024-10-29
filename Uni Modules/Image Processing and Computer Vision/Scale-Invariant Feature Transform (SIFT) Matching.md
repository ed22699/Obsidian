---
tags:
  - correspondence_matching
---
- two main elements:
	- scale invariant detection of salient (key) points
	- matching by highly distinct local descriptors
- key point detection:
	- extrema (max or min) in difference of Gaussian blurred versions of image $\rightarrow$ Difference-of-Gaussians (DoG) tree
	![[Screenshot 2024-10-29 at 13.17.19.png|300]]
		- most extrema present in both views possibly at different levels - scale invariance
	- points imaged at different resolutions appear at different levels of DoG tree $\rightarrow$ scale invariance
- spatial gradient descriptors:
	- built from histograms of spatial gradients in local neighbourhood
	- invariant to rotation and perspective warp (almost)
	![[Screenshot 2024-10-29 at 13.18.47.png|300]]
		- histograms built w.r.t. dominant orientation in region - rotation invariance (almost)
		- descriptor matching based on Euclidean distance between 128-D feature vectors
![[Screenshot 2024-10-29 at 13.22.19.png|300]]
![[Screenshot 2024-10-29 at 13.24.41.png|300]]
