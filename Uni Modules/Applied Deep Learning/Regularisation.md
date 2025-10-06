---
tags:
  - cost_regularisation_depth
---

- “Regularisation is any modification we make to a learning algorithm that is intended to reduce its generalisation error, but not its training error.” 
- many recent developments in deep learning are attempts to *reduce the complexity* of neural network training models, including
	- **L-regularisation**: constraining weight space
	- [[Dropout]]: stochastic network thinning
	- **depth**: composition over concatenation
	- parameter (CNNs) and network (RNNs) sharing
### L2-Regularisation
- *assumption*: target a local minimum with small-magnitude weights to combat overfitting
- *idea*: introduce a penalty for every weight based on its squared value directly in the cost function $J$
 ![[Screenshot 2025-10-06 at 16.57.20.png|400]]
 - practically, this is easiest implemented as scaled weight decay towards zero during training
 ![[Screenshot 2025-10-06 at 16.58.01.png|400]]
### L1-Regularisation
- *assumption*: we target a local minimum with *sparse weights* against overfitting (Occam's Razor)
- *idea*: introduce a penalty for every weight based on its magnitude directly in the cost function $J$
![[Screenshot 2025-10-06 at 16.59.38.png|400]]
- practically, this is easiest implemented as absolute weight decay towards zero during training
![[Screenshot 2025-10-06 at 17.00.11.png|400]]

- L2 is much more common and popular than L1, which is only really used in situations where you want *sparse weights*