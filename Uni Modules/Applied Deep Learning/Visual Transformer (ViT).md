---
tags:
  - rnn_transformers
---

![[Screenshot 2025-10-20 at 17.05.53.png|350]]
- image is converted to a sequence of tokens
	- done through breaking the image into patches and position embedding them
		- each patch is flattened into a 1D vector
		- linearly projected into a $D$-dimensional embedding $\rightarrow [x_1, x_2,...,x_N]$ 
		- positional embedding added to each patch to encode its position in the original image: $z_i = x_i +p_i$ 
			- where $p_i$ is the positional embedding for patch $i$
- CLS Token
	- after image is a sequence of patch embeddings, ViT prepends a special learnable token: $z_0 = [CLS]$ 
		- not derived from any image patch
		- learnt summary token for the entire image
- with self-attention, hopes to capture knowledge of the whole image
	- allows every token (including the CLS) to attend to every other token
	- CLS token aggregates information from all patches across all layers
	- by final layer, CLS token's embedding effectively represents a global summary of the entire image (captures most relevant features)
