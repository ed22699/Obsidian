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
- Neural networks often have many parameters (ChatGPT has 175 billion) so overfitting is an issue
- if we have a very large training dataset the problem is greatly reduced (GPT-3.5 used 570GB of data, about 300 billion words)
- There are also ways of reducing overfitting if we do not have this large training dataset:
### Early stopping
- create a validation set
- stop training when error on the validation set starts to increase
- using a validation set to prevent overfitting is not unique to neural networks
### Weight decay
- alter the loss function to penalise large weights
- also known as $\ell_{2}$ regularisation, adds a term $\lambda \boldsymbol{w}^{T}\boldsymbol{w}$ to the loss function, where $\boldsymbol{w}$ is the weight vector and the user chooses the value of $\lambda>0$
- in scikit-learn a parameter called $alpha$ sets $\lambda$ to $\frac{alpha}{N}$, where $N$ is the size of the training data. The default value of $alpha$ is $0.0001$, so we get a little $\ell_{2}$ regularisation
- since the loss we are trying to minimise is now not just about fitting the data, overfitting is reduced
### Dropout
![[Screenshot 2024-09-25 at 09.34.07.png|500]]
- where during training we randomly turn off all outgoing connections from a unit with some give probability $p$
- for each presentation of each training case, a new thinned network is sampled and trained
- each unit must learn to perform well even if some of the other units are missing at random. This prevents the units from learning complex, but fragile, dependencies on each other
- dropout can drastically reduce overfitting and is used a lot
# Missed
- have not looked into how the choice of architecture (neural network structure) is made
- recently been a lot of attention on attention (where the weights can depend on the input)
# Reading
- Murphy chapter 13
what is torch.nn really? 