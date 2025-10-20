---
tags:
  - rnn_transformers
---
- *Issue*: using Multi-Head Self Attention allows for $O(n^2)$ relations between items. However, there is no concept of order
	- some methods remove further attention weights, but this doesn't solve it
- *solution*: what if, alongside each input we passed in its timestamp
	- new issues:
		- this information represents a small part of the input
			- easy to ignore by the model
		- changing the size of the input, need to learn more weights
	- solution: add the output of a function to the input
$$
f_{0,i} = e(i)+x_i
$$
- where
	- $e(\cdot)$ is the positional encoding function that return a vector with the same length as $x_i$
		- how do we define this?
			- learnt encodings
			- non-learnt encodings
### Learnt Positional Encodings
- already learning a lot of parameters, what are a few 1000 more
- for an input embedding size of $d$
	- define $k$, $d$-length vectors for timesteps $0,1,...,k-1$
	- for $x_i$ simply return the $i^{th}$ vector
- requires knowing the maximum of a sequence beforehand
![[Drawing 2025-10-20 15.42.27.excalidraw|500]]
### Non-Learnt Positional Encodings
- generally used if you want to expand your sequences in testing
	- i.e. you don't know the potential maximum
- commonly, sinusoidal functions or fourier functions are used
- have useful repeating properties
#### Sinusoidal Positional Encodings
- a combination of `sin` and `cos` is used to define the vector
![[Screenshot 2025-10-20 at 15.51.24.png|150]]
- gives vectors such that the angle between them is consistent
	- i.e. $S(e_0, e_i) = S(e_k, e_{k+i})$
- means that relative distances can scale up to infinity
![[Screenshot 2025-10-20 at 15.52.33.png|300]]