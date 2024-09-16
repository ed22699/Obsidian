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
 ![[Shannon's Sampling Theorem]] 
## Modelling a Spatial Brightness Pulse 
![[Dirac Delta-Function ]]
![[Point Spread Function]]
## Colour Spaces
![[colourSpaces.png|500]]
in videos instead of $f[x,y]$ it is $f[x,y,t]$
### RGB 
- splits the image up into the intensities of the three main colours
- cons: strongly correlated channels, non-perceptual
### HSV 
![[HSV.png|400]]
- Hue: colour portion of the model, is a number from 0 to 360 degrees
- Saturation: describes the amount of gray in a particular colour from 0 to 100 percent
- Value: describes the brightness or intensity of the colour, from 0 to 100 percent
### CIE L\*a\*b\*
perceptually uniform colour space
- Luminance = brightness
- Chrominance = colour
- use Euclidean distances to represent colour differences

# Summary
- effect of vary sparse sampling is aliasing
	- anti-aliasing can be achieved by removing spatial frequencies above a critical limit (Shannon-Nyquist limit) [[Shannon's Sampling Theorem]]
	![[quantization.png|400]]
	