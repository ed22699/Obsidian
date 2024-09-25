---
tags:
  - Lesson
  - training
---
Once we have computed the gradient (at the current value of the weights) we can just send that gradient to an off-the-shelf gradient based optimiser to reduce error (on the training set). Sometimes this will not work as expected
# Problems
## Vanishing and exploding gradients 
- when training deep model the gradient can become very small (vanishing gradient problem) or very large ([[exploding gradient problem]])
## Residual Connections
- in a residual network each layer has the form of a residual layer defined as: $\mathcal{F}_{|}'(\boldsymbol{x}))= \mathcal{F}_{|}(\boldsymbol{x})+\boldsymbol{x}$
	- $\mathcal{F}_{|}(\boldsymbol{x})$ is the standard linear-activation-linear mapping
- weights defining $\mathcal{F}_{|}(\boldsymbol{x})$ learn what needs to be added to the input $\boldsymbol{x}$ 
- provides a short cut for gradient to flow directly from the output layer to any previous layer
![[Screenshot 2024-09-25 at 09.19.42.png|500]]
## Parameter Initialisation
- Neural network training is non-convex, i.e. the error landscape has many valleys and standard gradient descent just ends up at the bottom of whichever valley it happens to start in
- so choice of initial weights (parameter initialisation) matters
## Dealing with overfitting
### Early stopping
- create a validation set
- stop training when error on the validation set starts to increase
- using a validation set to prevent overfitting is not unique to neural networks
## Weight decay
- alter the loss function to penalise large weights
## Dropout
![[Screenshot 2024-09-25 at 09.34.07.png|500]]
- where during training we randomly turn off all outgoing connections from a unit with some give probability $p$
# Reading
- Murphy chapter 13
what is torch.nn really? 