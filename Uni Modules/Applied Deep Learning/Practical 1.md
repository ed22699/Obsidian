---
tags:
  - Lesson
---
- Pytorch and Tensorflow are the two main 
- Pytorch benefits
	- AutoGrad - automatic differentiation engine
	- More Pythonic
	- Everyone else uses it
- Use your GPU
![[Screenshot 2025-10-22 at 11.51.40.png|400]]
- training
	- loop through all *epochs*
		- *forward pass*: compute all layer outputs
		- calculate loss at final layer
		- *backward pass*: compute all delta gradients
		- update all weights
		- zero gradients 
- if it doesn't work just retrain