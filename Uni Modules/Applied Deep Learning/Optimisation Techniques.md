---
tags:
  - Lesson
---
- bad idea to take one sample at a time - lead to very noisy gradient descent
- DGD (deterministic gradient descent) is the opposite extreme
	- difficult because
		- limited memory on the GPU
		- may overfit if it is seeing everything all at once. Want to fit to the class not the data
- Middle ground is SGD