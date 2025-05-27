---
tags:
  - quantum_computing
---
## Manipulating data
- we still use gates
- most common gates are the X, Y and Z gates
	- X gate: flips the qubit $\pi$ radians around the x axis
		- $X = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$ 
	- Y gate: flips the qubit $\pi$ radians around the y axis
		- $Y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}$ 
	- Z gate: flips the qubit $\pi$ radians around the z axis
		- $Z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$ 
- these gates are their own inverses
![[Screenshot 2025-05-27 at 20.49.05.png|400]]
## Global and Relative phase
![[Screenshot 2025-05-27 at 20.54.19.png|300]]
- **global phase**: when the *entire qubit* is multiplies by a complex number
- **relative phase**: when *just one state* is multiplied by a complex number
- global phase is *irrelevant* as it is logically equivalent
 ![[Screenshot 2025-05-27 at 20.56.49.png|300]]
 - phase *does not effect the probability* or a 0 or 1
## Hadamard Gate and the +, -, i and -i states
![[Screenshot 2025-05-27 at 21.00.10.png|300]]
- Hadamard Gate: $H = \frac 1 {\sqrt 2} \begin{bmatrix} 1 & 1 \\ 1 & -1 \end{bmatrix}$ 
	- ![[Screenshot 2025-05-27 at 21.01.53.png|300]]
	- Hadamard gate is its own inverse
	- ![[Screenshot 2025-05-27 at 21.02.51.png|400]]
## Phase Gates S and T gates