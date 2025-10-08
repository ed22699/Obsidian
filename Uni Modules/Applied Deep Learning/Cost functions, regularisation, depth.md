---
tags:
  - Lesson
---
## Key Cost Functions
- we want outputs to represent probabilities of class labels, thus outputs should be within {0,1} and sum to 1
- we can force outputs to reflect such a distribution by creating a layer-wide, normalising non-linearity
	- introduce a *softmax neuron group* in the last layer with
$$
g_j^N(s_j^N)= \frac {e^{s_j^N}}{\sum_{i \in group} e^{s_i^N}}
$$
$$
g_j^{'N}(s_j^N)=f_j^N(1-f_j^N); g_j^{'N}(s_{i \neq j}^N)=-f_j^Nf_i^N
$$
- now all outputs $f_i^N$ range between 0 and 1, while the group output sums to 1
- for an appropriate cost function use *cross-entropy* as the group's cost function
![[Screenshot 2025-10-08 at 16.02.09.png|500]]
![[Screenshot 2025-10-08 at 16.03.10.png|500]]
![[Screenshot 2025-10-08 at 16.04.07.png|400]]
![[Screenshot 2025-10-08 at 16.04.35.png|400]]

## Regularisation
![[Regularisation]]
## Dropout
![[Dropout]]
## Data Augmentation
![[Screenshot 2025-10-08 at 16.17.27.png|400]]
## Why Deep and Scalability
![[Screenshot 2025-10-08 at 16.18.50.png|500]]
![[Screenshot 2025-10-08 at 16.19.37.png|400]]
![[Screenshot 2025-10-08 at 16.20.03.png|400]]
![[Screenshot 2025-10-08 at 16.20.55.png|400]]