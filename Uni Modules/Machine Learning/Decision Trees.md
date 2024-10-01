---
tags:
  - Lesson
  - trees
---
# Decision Trees
![[Screenshot 2024-10-01 at 11.05.25.png|300]]
- one model is responsible for assigning a decision for each region of input space
- correct model for an input $x$ is chosen by traversing the binary decision tree, following the path from the top to a leaf
- leaf node is responsible for assigning a decision, such as a:
	- class label
	- probability distribution over class labels
	- scalar value (for regression tasks)
- aims to greedily minimise the error
	- regression: sum-of-squares
	- classification: cross-entropy as used in neural networks or Gini impurity
	- add nodes one-at-a-time, choosing the best splits at each point
	1. start from the root node
	2. run exhaustive search over each possible variable and threshold for a new node. For each variable and threshold:
		1. computer average of the target variable for each leaf of the proposed node
		2. compute the error if we stop adding nodes here
	3. choose the variable and threshold that minimise the error
	4. add a new node for the chosen variable and threshold
	5. repeat step 2 until there are only $n$ data points associated with each leaf node
	6. prune back the tree to remove branches that do not reduce error by more than a small tolerance value, $\epsilon$ 
- number of possible solutions grows combinatorially with the number of input variables
## Interpretability
- often easier to interpret than other methods (such as neural networks)
- however, sometime small changes to the dataset cause big changes to the tree
- if the optimal decision boundary is not aligned with the axes of an input variable, we need a lot of splits
	![[Screenshot 2024-10-01 at 11.21.05.png|200]]

## Pruning
- need to balance training-set error against model complexity
	1. start with a tree $T_0$, consider pruning each node in $T_0$ by combining the branches to obtain tree $T$ 
	2. compute a criterion $C(T)=\sum_{T=1}^{|T|}e_T(T)+\lambda|T|$ 
		- use cross validation or a validation set to select a $\lambda$ 
	3. if $C(T)\leq C(T_0)$ keep the pruned tree, else reinstate the pruned node
	

# Reading
- Bishop 14.4 (note typo missing a minus sign p666 equation 14.32)