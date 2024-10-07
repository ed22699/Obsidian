---
tags:
  - Lesson
  - viola_jones_detector
---
Viola-Jones detector is a sliding window detector
## Harr-like Features
![[Harr-like Features]]
## Integral Image
![[Integral Image]]
## Viola & Jones' Real-time Method
- have a collection of many [[Harr-like Features]] and pass them all over an image via [[sliding window detectors]]
### Training
![[Screenshot 2024-10-07 at 15.44.34.png|400]]
**AdaBoost Classifier**
- combine multiple weak classifiers to form a stronger predictive model
	- sequentially train weak classifiers, focusing more on instances that were previously misclassified (weak learner)
	- combine their outputs to create a more accurate final classifier (boosting idea)
![[Screenshot 2024-10-07 at 15.46.14.png|400]]
