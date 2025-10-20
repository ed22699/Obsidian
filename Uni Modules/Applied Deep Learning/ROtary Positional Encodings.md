---
tags:
  - rnn_transformers
---
- an extension of relative positional encodings
## Relative Positional Encodings
- non-learnt positional encodings that represent the relative positions between inputs
- each pair of words has a different positional encoding
![[Drawing 2025-10-20 16.17.59.excalidraw|500]]
![[Screenshot 2025-10-20 at 16.20.24.png|400]]
- in practice it's a lot of information for the model to try and learn around
	- slow to calculate from a performance point of view
## ROtary Positional Encoding
- an extension of relative positional encodings
- instead of adding the positional encoding to the vector we want to rotate the vector by an angle $\theta$
![[Screenshot 2025-10-20 at 17.01.29.png|250]]
![[Screenshot 2025-10-20 at 17.02.07.png|500]]
- this means that the inputs to the transformer are more stable
- easier for the model to learn what position represents
- standard for most modern LLMs
- easier for the model to learn because its just doing one rotation
![[Drawing 2025-10-20 16.28.44.excalidraw|600]]
