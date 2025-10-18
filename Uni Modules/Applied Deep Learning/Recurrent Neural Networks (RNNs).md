---
tags:
  - rnn_transformers
---
![[Screenshot 2025-10-18 at 15.39.35.png|300]]
- what is this hidden state
	- some representation of what's happened in the past
	- thought of as some lossy memory that gets updated at every timestep with the most important information
![[Screenshot 2025-10-18 at 15.40.55.png|300]]
- you can think of $W$ and $\phi$ as a normal network
	- you're just saving/adding in a saved state
![[Screenshot 2025-10-18 at 15.41.47.png|200]]
$$
h_t = f(h_{t-1},x_t;W,\theta)
$$
- where $t$ are differing timesteps
- $f$ and $\theta$ are shared across all timesteps
$$
O_t=g(h_t;\phi)
$$
$$
O_t = g(f(h_{t-1}, x_t; \theta); \phi)
$$
![[Screenshot 2025-10-18 at 15.45.21.png|400]]
- to perform the backward pass we need to backpropagate to the first input
- depending on the length of the input this could be excessive
- this is known as the *Back-Propagation Through Time (BPTT) algorithm*
![[Screenshot 2025-10-18 at 15.47.03.png|400]]
- auto-differentiation for RNNs haven't changed as long as you accumulate gradients, this is the same as for CNNs, just a bigger graph
## RNN Types
- original RNN as described above
	- the triangles shown below could be anything, not just a FC layer
	- keeps track of a saved/hidden state
	- we don't use the output instead of the saved state as it is less powerful, $O_i$ is generally a low dimension representation
![[Screenshot 2025-10-18 at 15.49.41.png|200]]
- if we don't care about the outputs of anything but thee last
	- is useful to produce summaries
	- is useful as part of an encoder/decoder
![[Screenshot 2025-10-18 at 15.52.39.png|200]]
- if we want to translate from one language to another
	- assume there's some common semantic space between them
	- translate into a universal language space then translate to a different language
![[Screenshot 2025-10-18 at 15.54.20.png|400]]
![[Screenshot 2025-10-18 at 15.54.37.png|300]]
![[Screenshot 2025-10-18 at 15.54.59.png|400]]