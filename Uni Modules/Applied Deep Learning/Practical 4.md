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
	- random noise
	- occlusion
	- time of year
- CutMix is a new tool to try and augment data by mixing
	- has benefit of having localised areas
## Debugging
- we don't know what numbers to expect when training a method so careful debugging is a must
- check baseline performance 
	- the random performance of an $n$-way classifier will be $\frac 1 n$%
- check for imbalanced classes
	- common baseline is majority class
		- predict only the class with most examples
- check the structure of the network - is it as you have written it?
- check your input - both data and labels
	- easy to pass in the wrong index or not use all of your input
- check your initialisation 
	- with random initialisation you can work out the expected value for your loss
- start simple and break up your model
- check with a small amount of data first (mickey mouse examples)
	- if your model cannot fit to 10s of examples don't expect it to work on 1000s
- save checkpoints and models frequently
	- general practice to save every X epochs in addition to the best performance
## Dropout
- during training, each node has a $1-p$ chance of being removed
	- their outputs are set to 0
- during testing, outputs are multiplied by $p$ to ensure similar magnitudes within the network