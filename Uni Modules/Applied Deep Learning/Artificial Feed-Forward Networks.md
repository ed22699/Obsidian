---
tags:
  - basic_neural
---
## Perceptron (1950s)
![[Screenshot 2025-09-27 at 11.58.08.png|400]]
![[Screenshot 2025-09-27 at 11.59.15.png|500]]
![[Screenshot 2025-09-27 at 12.00.10.png|500]]
- is a form of linear classification, the first perceptron originally decided if something was on the left, or right hand side of a page. It then progressed onto detecting triangles to circles
### Basic Perceptron (Supervised) Learning Rule
- whenever the system produces a misclassification with current weights, adjust weights by $\Delta w$ towards a better performing weight vector
$$
\underbrace{\Delta w}_{update} = \begin{cases}
\eta f^*(x)x & if \; \overbrace{f^*(x)}^{ground \; truth} \neq \overbrace{f(x)}^{actual \; output} \\
0 & otherwise
\end{cases}
$$
- where $\eta$ is the learning rate
![[Screenshot 2025-09-27 at 12.09.28.png|400]]
![[Screenshot 2025-09-27 at 12.09.59.png|400]]
![[Screenshot 2025-09-27 at 12.10.30.png|400]]
## Cost (or Loss) Functions
- given a set $\textbf{X}$ of input vectors $\textbf{x}$ of one or more variables and a parameterisation $\textbf{w}$, a Cost Function is a map $\textbf J$ onto a real number representing a cost or loss associated with the input configurations
	- negatively related to goodness of fit
- expected loss: $J(X;w)=E_{(x,f^* (x)) \sim p} L(f(x;w), f^* (x))$
- empirical risk: $J(X;w) = \frac 1 {|X|} \sum_{x \in X} L(f(x;w), f^* (x))$
- MSE Example: $MSE_{loss} = \underbrace{J(X;w)}_{loss \; function} = \frac 1 {|X|}\sum_{x\in X}\underbrace{(f(x;w) - f^* (x))^2}_{per-example \; loss \; function}$
## Steepest Gradient Descent
![[Screenshot 2025-09-27 at 12.18.20.png|500]]
- goal is to find the minimal cost function in the parameter plane, for this the aim is to traverse down in gradient to find this lowest point
$$
\underbrace{w_{t+1}}_{new} = \underbrace{w_t}_{old}-\underbrace{\eta}_{learning \; rate} \underbrace{\nabla J (X;w_t)}_{steepest \; gradient}
$$
### The Delta Rule
![[Screenshot 2025-09-27 at 12.24.04.png|500]]
## Linear Separability
- the first issue with the perceptron came when attempting to classify and XOR, this is a non-linearly separable problem, so the perceptron simply could not handle it alone
![[Screenshot 2025-09-27 at 12.25.57.png|400]]
- *Solution:* use a multi-layers perceptron (MLP) with non-linear activation functions
![[Screenshot 2025-09-27 at 12.26.52.png|400]]
## Multi-Layer Architectures
![[Multi-Layer Architectures]]