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
- memory inefficiency
- lack of flexibility 
- computational inefficiency 
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
- for an image, INRs learn a function $f: \mathbb R$  --- **stopped notes here**