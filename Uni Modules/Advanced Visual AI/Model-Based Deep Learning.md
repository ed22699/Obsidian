---
tags:
  - Lesson
---
- note soft thresholding
## Deep Image Prior (DIP)
- idea: A randomly initialised neural network can be used as handcrafted prior for solving imaging inverse problems
- not fully model based not fully neural network
	- middle ground between learning-based, data-driven methods, which use deep convolutional neural networks and classical model-based approaches involving handcrafted image priors
	- relies on both but doesn't need tonnes of data
- start with sample of pure noise ($z$) that you pass through a neural network, you get $f_{\theta _0}(z)$. Take that output of the neural network together with the image you want to enhance. Calculate the distance between the neural network output and the image ($x_0$). Take the gradient of that distance and backpropogate it back in. You repeat this until you get a very similar image to that which you wanted to de-noise 
	- you need to find the right moment to stop, stop in the bottom of the curve before you start reconstructing noise

- assuming a good choice of $g$, DIP gets rid of the prior and puts in a neural network $f_\theta (z)$ 