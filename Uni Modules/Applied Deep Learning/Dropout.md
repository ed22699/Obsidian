---
tags:
  - cost_regularisation_depth
---
![[Screenshot 2025-10-08 at 16.05.05.png|400]]
## Dropout for regularisation
- *idea*: during training, for each loop of weight updates immobilise a random subset of neurons with probability $(1-p)$ by forcing their output to zero (particularly effective when applied to final fully-connected layers of networks)
	- these neurons now do not contribute to the network output nor can thy be used for adjusting weights or passing gradients through them; $p$ is often set to a value around $0.5$ before tuning on validation data
	- makes a more robust model and combats overfitting
![[Screenshot 2025-10-08 at 16.09.02.png|400]]
![[Screenshot 2025-10-08 at 16.10.07.png|400]]
## DropConnect
![[Screenshot 2025-10-08 at 16.10.27.png|400]]
- *idea*: instead of dropping neurons, DropConnect sets sets weights to zero with a probability $(1-p)$ providing a more fine-grained mechanism for regularisation based on the same underlying concept
## Data against overfitting
- overfitting can always be addressed b y more data, more representative data and/or strategically sampled data
	- given the high dimensionality of deep net parameter spaces, taking advantage of more data is often possible without reaching the representational limits of the network