---
tags:
  - Lesson
  - object_detection
---
aims at bridging the 'semantic gap' between 
- given pixel values
- meaningful objects (grouping of pixels + classification of groups)

- image regions need to be found and assigned with semantic labels from a space of object classes
- classical shape detection and segmentation on their own rarely work for real-world object detection as:
	- high intra-class variance
	- low inter-class variance
	- classes are rarely well defined
	- change of illumination, scale, pose, deformation, occlusion, etc
	![[Screenshot 2024-10-04 at 16.38.15.png|300]]
## Techniques
 ![[line and circle detection]]
![[colour-based detection]]
![[classifiers with sliding window detectors]]
![[template matching]]
![[Point Feature Matching]]
![[Optical Character Recognition]]
![[deep learning-based object detectors (out of scope or unit)]]