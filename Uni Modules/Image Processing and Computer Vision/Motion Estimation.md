---
tags:
  - Lesson
  - motion_estimation
---
assume optical flow results from brightness constancy constraint
- natural to assume, if we are taking enough frames per second this is a valid assumption as there will only be small changes. With larger gaps between frames, illumination can effect this

you can only predict the motion perpendicular to the edge (you can only be sure of $u_n$ in normal flow) $\rightarrow$ aperture problem
- aperture is a region within our frame where we are viewing this motion
- why don't I make very big aperture?
	- motion in a scene typically has motion going in different directions, this will be lost with a big aperture
- why don't I make a very small aperture
	- motion with potentially each pixel, within the entire image due to depth, etc, leads to a lot of motion which you can't do much with
predicting motion is bad when it comes to edge as will suddenly have a large depth between two points so will be viewed as a large change

$A$ will not have an inverse when our region is over an edge
- will not have an inverse is determinant of $A$ is $0$ 
issue when motion within the region is all in different directions