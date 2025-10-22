---
tags:
  - Lesson
---
- DL models are data hungry
- collecting data is time consuming and expensive
![[Screenshot 2025-10-22 at 12.23.49.png|350]]
- if you collect more data and nothing improves
	- check the quality of the data and its labels
- we can get more data by just generating our own from what we have
	- need to be careful about invariances
## Object Invariances
- for object recognition we have the following invariances
	- horizontal flip
	- crop (scale)
	- rotation
	- vertical flip
	- variable brightness
	- greyscale
## Action Invariances
- depending on the label granularity, some transformations aren't invariant
- we can generate data by applying transformations that are invariant to the semantic label
	- called *data augmentation*
## Data Augmentation
- transformations applied to the data should not change the labels
- a standard practice for all methods to generalise better
- other invariances
	- 