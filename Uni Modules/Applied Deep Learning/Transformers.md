---
tags:
  - rnn_transformers
---
- state of the art
- original 2017 paper cited over 132k times
- originally developed for NLP - vision/audio are also now used
- RNNs and other recurrent models use the concept of history
	- is lossy, not everything can be saves kept between timesteps
## Many-To-Many Relationships
- instead of keeping track of a history, transformers simply relate everything to everything
	- i.e. in the calculation we want to find how the information at every timestep influences information at every other timestep
![[Screenshot 2025-10-18 at 15.58.43.png|400]]
- *issue*: expensive but overwhelmingly powerful
	- requires
		- more data
		- more parameters
		- more resources

![[Attention]]

## Positional Encodings
![[Positional Encodings]]
![[Screenshot 2025-10-20 at 15.53.13.png|500]]
## ROtary Positional Encodings
![[ROtary Positional Encodings]]
## Visual Transformer (ViT)
![[Visual Transformer (ViT)]]
