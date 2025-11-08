---
tags:
  - Lesson
---
- taking image and turning it into a 3D model
# Discrete Representations
- existing 3D representations discretise the output space differently
	- spatially in voxel representations
	- in terms of predicted points
	- in terms of vertices for mesh representations
## Limitations of Discrete Representations
- Resolution limitations
	- *fixed grid resolution* limits detail, requiring significantly more memory to increase fidelity
	- *fine details and smooth surfaces are difficult to capture*, leading to blocky or jagged artefacts
- memory inefficiency
	- *exponential memory growth* in 3D as resolution increases
	- many *regions in 3D spaces are sparse*, wasting memory in empty areas
- lack of flexibility 
	- fixed resolution across the entire shape, unable to dynamically adjust detail
	- real-world shapes are inherently continuous, making discrete grids unnatural for detailed representations
- computational inefficiency 
	- operations on large grids are computationally expensive
	- scaling to high resolution becomes infeasible for real-time applications
# Implicit Representation
- offer a flexible approach to 3D modelling, avoiding discretisation limitations
- support arbitrary topology and resolution, enabling detailed and complex shapes without fixed structures
- *Issue*: Given a complex signal, finding an exact function $f$ that represents it continuously is challenging
	- such functions are often "too complex to simply write them down"
- *Solution*: Implicit neural representations
	- neural networks (e.g. MLPs) are used to estimate this function $f$
	- trained on discrete samples of a signal, neural networks learn to approximate the continuous function $f$, denoted as $\mathcal F$ 
- network parameterises $\mathcal F$, with $f$ implicitly encoded in the network after training - hence the term *Implicit Neural Representation*
## Mappings in 2D (Images)
- for an image, INRs learn a function $f: \mathbb R^2 \rightarrow \mathbb R^3$ that maps each spatial coordinate $(x,y)$ to an RGB colour value
	- $f(x,y) = \begin{bmatrix}R \\ G \\ B \end{bmatrix}$
	- where $f(x,y)$ outputs the red, green and blue values for each pixel coordinate $(x,y)$
### Implicit Neural Representation Model
![[Implicit Neural Representation Model]]
