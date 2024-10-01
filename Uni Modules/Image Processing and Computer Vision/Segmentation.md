---
tags:
  - Lesson
  - segmentation
---
is the process of spatial sub-sectioning of a (digital) image into multiple partitions of pixels (i.e. segments or regions) according to given criteria
![[Screenshot 2024-10-01 at 11.35.57.png|300]]
why?
- image simplification 
	- image may contain millions of pixels but only a few regions
- higher-level object description
	- regions tend to belong to the same class of object
	- regions may provide object properties (e.g. shape, colour)
- input for content classifiers
	- region descriptions can be input data for higher level classifiers, e.g. Bayesian Classifiers or Neural Networks
goals
- gather pixels/features that belong together
- obtain an intermediate representation that compactly describes key image parts
**Top-down**:
- pixels belong together because they are from the same object
**Bottom-up**:
- pixels belong together because they look similar
![[Over-segmentation]]
![[Under-segmentation]]
# Segmentation Methods
- ![[Thresholding methods]]
- Edge-based methods
	- region boundaries are constructed from edge-maps
- ![[Region-based methods]]
- ![[Clustering and Statistical methods]]
- Topographic methods (not scope of unit)
	- stepwise simplifications that take spatially wider (topographical) image configurations into account e.g. watershed transform, variational based methods