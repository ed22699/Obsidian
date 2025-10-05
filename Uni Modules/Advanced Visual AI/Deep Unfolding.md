---
tags:
  - model_based_deep
---
- also referred to as deep unrolling
- converts an iterative algorithm into a DNN by designing each layer to resemble a single iteration
- application of deep unfolding to design a model-aided deep network is based on the following steps:
	1. identify an iterative optimisation algorithm that is useful for the problem at hand
	2. fix the number of iterations of the optimisation algorithm 
	3. design the layers to imitate the free parameters of each iteration in a trainable fashion
	4. train the overall resulting network end-to-end
![[Screenshot 2025-10-05 at 19.19.11.png|500]]