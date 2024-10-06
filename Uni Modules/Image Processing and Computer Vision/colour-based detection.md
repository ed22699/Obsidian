---
tags:
  - object_detection
---
in some cases, objects can be detected based on their colour properties. This is especially useful when objects have distinct and consistent colours
![[Screenshot 2024-10-05 at 14.55.26.png|400]]
### Morphological Operations
#### Erosion
- the erosion of $A$ by $B$ is defined by: $A \ominus B = \{z|B_z \subseteq A\}$ 
- it is the set of pixel locations $z$ that overlap with foreground pixels in $A$
- $B = \begin{bmatrix}1 & 1& 1\\1&1&1\\1&1&1\end{bmatrix}$
![[Drawing 2024-10-05 15.01.34.excalidraw|300]]
#### Dilation
- the dilation of $A$ by $B$ is defined by : $A \oplus B = \{x|(\hat{B})_z \cap A \neq \varnothing\}$ 
- $\hat{B}$ is the reflection of the structuring element $B$ 
![[Drawing 2024-10-05 15.14.59.excalidraw|300]]
![[Screenshot 2024-10-05 at 15.17.29.png|300]]
