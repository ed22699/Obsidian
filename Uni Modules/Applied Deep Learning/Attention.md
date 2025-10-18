---
tags:
  - rnn_transformers
---
- get networks to focus on certain inputs
	- standard linear layer is given by: $y=Wx+b$
	- we want to learn how important each dimension is
$$
y = x \odot \sigma (Wx+b)
$$
- where
	- $\sigma$ is the softmax function 
![[Drawing 2025-10-18 16.09.08.excalidraw|400]]
## Attention Maps
- if we know the attention weights, we can work out what areas a model is focusing on
	- called attention maps
![[Screenshot 2025-10-18 at 16.26.21.png|600]]
## Self-Attention
- we have data in an ordered sequence
- self-attention allows us to calculate how certain elements will be more/less relevant to others
	- "look at other inputs to better encode my own input"
	- for $n$ inputs, create an $n \times n$ grid of attentions to apply for each input
	![[Screenshot 2025-10-18 at 16.29.27.png|150]]
![[Screenshot 2025-10-18 at 16.28.30.png|200]]
- given the formula we apply self-attention through introducing the terms Query, Key and Value and drop the bias term
	- we define each as a *projection* of the input
		- allows for better modelling as we're not using the base input
![[Screenshot 2025-10-18 at 16.33.54.png|300]]
![[Drawing 2025-10-18 16.34.51.excalidraw|400]]
- $\sqrt d$ is good to smooth it a little make the query to key nice

slide 51
