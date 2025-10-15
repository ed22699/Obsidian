---
tags:
  - generative_ai
---
### Conditioning with class
- guiding the generation process using extra information
![[Screenshot 2025-10-15 at 09.24.17.png|250]]
$$
\mathbb E_x [\log (D(x,c))] + \mathbb E_z[\log (1-D(G(z,c),c))]
$$
![[Screenshot 2025-10-15 at 09.23.59.png|300]]
### Conditioning with image: Image-to-image translation
![[Screenshot 2025-10-15 at 15.24.32.png|500]]
### Pix2Pix
![[Screenshot 2025-10-15 at 15.25.00.png|500]]
- u-net is an encoder-decoder but with a skip connection between each encoder block and its corresponding decoder block at teh same resolution 
	- skips concatenate or add feature maps from encoder layers to decoder layers
	- decoder gets both the coarse, abstract features from the bottleneck and the fine, spatially aligned features from earlier encoder layers
	- skip connections preserve spatial detail lost during downsampling
	- often leads to sharper outputs and better localisation
- adding noise helps with robustness
	- also ensures more individual outputs with slight differences
- we use the absolute error rather than MSE as it is more robust
	- MSE will change the network too much with outliers, such as if a pixel is slightly offset it will blow up the error
## Unpaired image-to-image translation
### CycleGAN
- Cycle-Consistent Generative Adversarial Networks, is a modification of GAN that can be used for image-to-image translation tasks where paired training data is not available
- the algorithm can learn to convert an image from X into Y, as well as an image from Y into X, without any specific order or pairing between the images in the two collections
![[Screenshot 2025-10-15 at 15.37.04.png|200]]
- background of zebra from horse example grass was more brown, this is because zebra lives in dryer grassland, this low level feature of the training images ultimately got passed through to the translation from horse to zebra
### Training
![[Screenshot 2025-10-15 at 15.37.59.png|400]]
![[Screenshot 2025-10-15 at 15.38.21.png|500]]
- used a lot in medical images
	- means you can use a low-dose CT scan that would include more noise and use a generator that is trained on high-dose CT scans to remove the noise
![[Screenshot 2025-10-15 at 15.38.40.png|300]]
- can enhance video of low light using example of what images of the scene would look like in normal lighting