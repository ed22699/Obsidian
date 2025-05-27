- is a quick computer that utilises quantum mechanics
## Mathematical Prerequisites
### Complex numbers
- standard form: $a +ib$, where $a, b \in \mathcal R$ 
- $i^2 = -1$
- complex conjugate: $a+ib = (a+ib)^* = a - ib$ 
	- $(a+ib)(a-ib) = a^2 + b^2$
	![[Screenshot 2025-05-27 at 20.12.33.png|400]]
	- exponential form: $re^{i\theta}$ 
- in quantum computing exponential from is the main method as you rotate round a circle
### Basic linear algebra 
- column vector to represent the state of the quantum computer
- unitary matrices: $U^\dagger U = I$ 
	- when acting on a vector, unitary matrices rotate/flip the vector, keeping the magnitude of the vector the same
- Hermitian Matrices: $H = H^\dagger$ 
## Introduction to the Qubit and Superposition
 - quantum computers use quantum bits (can be 0 and 1 at the same time)
	 - can be any quantum particle that has 2 distinct states, such as a photon of light being polarised either horizontally or vertically
- still use 0's and 1's: $|0\rangle = \begin{pmatrix}1 \\ 0 \end{pmatrix}, |1\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$ 
- superposition: quantum particle is in two states simultaneously 
- $|\psi \rangle = \begin{pmatrix}\alpha \\ \beta \end{pmatrix}$ 
	- $\alpha$ represents how much the qubit is in the $|0\rangle$ state
	- $\beta$ represents how much the qubit is in the $|1\rangle$ state
- when we measure a quantum system, it collapses into the measured state
	- when you measure a superposition it will become either 1 or 0
	- the reason you still have the $\alpha$ and $\beta$ is because it helps us find the probability of it either collapsing into a 0 or 1
		- $P(|\psi\rangle = 0) = |\alpha|^2$
		- $P(|\psi\rangle = 1) = |\beta|^2$
		- $|\alpha|^2 + |\beta|^2 = 1$ 
## Dirac Notation
- $|\psi \rangle = \begin{pmatrix} \alpha \\ \beta \end{pmatrix} = \alpha |0\rangle + \beta |1\rangle$, this is the Dirac notation
	- conventional way of writing a quantum computing state
## Bloch Sphere
![[Screenshot 2025-05-27 at 20.42.04.png|400]]
- higher vertically = higher probability of measuring as $|0\rangle$
- lower vertically = higher probability of measuring as $|1\rangle$
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
- global phase: when the entire qubit is multiplies by a complex number
- relative phase: when just one state is multiplied by a complex number
- global phase is *irrelevant* as it is logically equivalent
 ![[Screenshot 2025-05-27 at 20.56.49.png|300]]
 - phase does not effect the probability or a 0 or 1
## Hadamard Gate and the +, -, i and -i states
![[Screenshot 2025-05-27 at 21.00.10.png|300]]
- Hadamard Gate: 