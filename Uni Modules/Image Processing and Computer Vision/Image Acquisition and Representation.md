---
tags:
  - Lesson
  - Image_A_And_R
---
- Image processing is the digital manipulation of an image to enhance it or extract some useful information from it for further processing
- Computer vision attempts to bridge the semantic gap between pixels and their meanings
$$
Pixels \to Features \to Models \to Meaning
$$
## Challenges
- View-point variation (the angle)
- Illumination
- Occlusion (things in front of others)
- Scale
- Deformation ----
- Background clutter ------
- Object intra-class variation (variations of an object type)
- Local ambiguity (similar looking images)
![[imageSamplingQuantisation.png|700]]
## [[Shannon's Sampling Theorem]] 
## Modelling a Spatial Brightness Pulse 
![[Dirac Delta-Function ]]
## The Point Spread Function
![[Screenshot 2024-09-16 at 17.42.14.png|300]]
- ideally, the optical system should be mapping point information to points again, however, optical systems are never ideal
- superposition principle : an image is the sum of the PSF of all its points
if $f(x,y)$ is the original, $g(x, y)$ is the 
## Colour Spaces
### RGB ---
### HSV ---
- Hue
- Saturation
- Value
### CIE -----