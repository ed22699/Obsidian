---
tags:
  - Lesson
---
- an image is worth $\sim 3,000$ words
	- each image is $32\times 32$ pixels
	- with three channels (RGB)
	- leads to $32\times 32 \times 3 = 3,072$ pixels of information
### Building CNN
- first convolutional layer includes a filter of size $5 \times 5 \times 3$ (76 weights)
- multiple filters allow for different specialisms
	- with 32 filters we now have a block of $32\times 32\times 32$
		- weights now $(5\times5\times3 + 1)\times 32 = 2,400$
- after an activation function, we perform pooling on $2\times 2$ grids
	- done over all the output layers
- second convolutional layer
	- with 64 filters this time
		- weights now $(5\times5\times32+1)\times 64 = 51,200$
 - second $2\times2$ pooling layer added	
 - reshape for FC layers
 - final projection into 10 classes
 ![[Screenshot 2025-10-22 at 12.08.56.png|500]]
 ![[Screenshot 2025-10-22 at 12.10.11.png|200]]