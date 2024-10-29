---
tags:
  - Lesson
  - correspondence_matching
---
# Stereo Correspondence
![[Screenshot 2024-10-29 at 12.25.34.png|200]]
## Region-Based Methods
![[Screenshot 2024-10-29 at 12.28.33.png|200]]
- compare pixel values within regions in two views
	- for region in left image, compute similarity with regions of same size in right image
- corresponding point - centre of most similar region
- trouble areas:
	- self occlusion
	- scale issue with distance
	- angle can warp image
	- occlusion with other objects
- stereo image pair: $I_L(x,y)$ and $I_R(x,y)$
- for each pixel, find disparity $d=(d_x, d_y)$ which minimises (or maximises) cost function
	- $c(\boldsymbol{d})=\sum_{(i,j)\in W(x,y)}s[I_L(i,j),I_R(i+d_x,j+d_y)]$
		![[Screenshot 2024-10-29 at 12.35.38.png|300]]
		- $W(x,y) \Rightarrow$ window of pixels around $(x,y)$
		- $s$ is the similarity measure
			- sum fo squared differences: $s(u,v)=(u-v)^2$
			- similar pixel count: $s(u,v)=\begin{cases}1 && if|u-v|<T\\0 && else\end{cases}$
			- normalised cross correlation: $s(u,v)=\frac{(u-\bar{u})(v-\bar{v})}{N_uN_v}$
				- $\bar u =\frac 1 {|W|} \sum_{u\in W}u$ (mean)
				- $N_u=\sqrt{\sum_{u\in W}(u-\bar u)^2}$ (standard deviation)
				- takes into account the regions themselves
				- normalised cross correlation means change in luminosity between two of the same patterns will not have an affect unlike with sum of squared differences and similar pixel count where it will score low
- problem with region-based is that you will often be comparing regions that are hard to compare
## Feature-Based Methods
- busy regions have a lot of variation, plain regions are harder to find a match so we search for these busy regions to use for a match
- restrict search to sparse set of features
	- reduces mismatches caused by texture-less regions
- find salient (distinct) points in each view and match points by comparing pixels or image descriptors in local regions about each point
- examples:
	- [[Harris corner detector]] (salient points)
	- [[Scale-Invariant Feature Transform (SIFT) Matching]]
	- typically use salient points followed by SIFT matching
### Where to look - Calibrated
- for calibrated stereo set up, corresponding points lie on epipolar lines
	- given point in left image, search for point in right image along band about epipolar line
	- increases speed, reduces mismatches




