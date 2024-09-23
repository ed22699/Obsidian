---
tags:
  - Lesson
  - neural_networks
---
# Perceptron (simplified neural network)
- directly inspired by how neurons process information
![[Screenshot 2024-09-23 at 11.22.57.png|200]]
- example of [[Linear Discriminant Function]] given by $y(x) = f(w^{T}\phi(x))$ with a nonlinear activation function$f(a) = \begin{cases} +1 & a \geq 0 \\ -1 & a < 0\end{cases}$
- target $t=\{+1, -1\}$
- aim to minimise the following error: $-\sum_{n=1}^{N}\boldsymbol{w}^{T}\phi_{n}t_{n}$
- sigmoid function: $\phi(x) = \frac{1}{1+e^{-x}}$
## Multiple Layer Perceptron (MLP)
![[Screenshot 2024-09-23 at 11.32.13.png|400]]
>[!note] 
>despite both being denoted by $w$ here the first and the second weight vectors will be different
- neural networks are composite functions of linear-nonlinear functions
- deep learning refers to neural networks (or MLPs) with more than 1 hidden layer
- MLP recipe:
- define architecture (i.e. how many hidden layers and neurons)
- define cost function (e.g. mean squared error)
- optimise network using backprop:
	1. [[forward pass]] - calculate activations; generate $y_{k}$
	2. calculate error/cost function
	3. backwards pass - use [[back-propagation]] to compute error gradient
	4. use gradient to improve parameters
![[gradient descent]]

- as MLPs are highly flexible they can easily overfit
	- you can solve this with early stopping (stop when test performance starts decreasing) and regularisation methods such as dropout (randomly turn off units during training)
![[Screenshot 2024-09-23 at 13.25.35.png]]
# Reading
- Bishop 5.1 except 5.1.1
- Bishop 5.2 except 5.2.2
- Bishop 5.3 up to 5.3.2