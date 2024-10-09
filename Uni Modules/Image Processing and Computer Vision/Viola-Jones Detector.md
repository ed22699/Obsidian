---
tags:
  - Lesson
  - viola_jones_detector
---
Viola-Jones detector is a sliding window detector
## Harr-like Features
![[Harr-like Features]]
## Integral Image
![[Integral Image]]
## Viola & Jones' Real-time Method
- have a collection of many [[Harr-like Features]] and pass them all over an image via [[sliding window detectors]]
### Training
![[Screenshot 2024-10-07 at 15.44.34.png|400]]
**AdaBoost Classifier**
- combine multiple weak classifiers to form a stronger predictive model
	- sequentially train weak classifiers, focusing more on instances that were previously misclassified (weak learner)
	- combine their outputs to create a more accurate final classifier (boosting idea)
![[Screenshot 2024-10-07 at 15.46.14.png|400]]
**Algorithm**
1. initialise weights
	- initially all given equal weight ($w_i=\frac 1 n$)
2. train a weak learner
	- weak learner $h_t(x)$ (e.g. decision stump) is trained on weighted dataset
	- weak learner makes predictors on the training data, and its classification error $\varepsilon_t$ is calculated: $\varepsilon_t=\frac{\sum_{i=1}^nw_i\cdot \boldsymbol{I}(h_t(x_i)\neq y_i)}{\sum_{i=1}^nw_i}$ 
		- $\boldsymbol{I}$ is an indicator function that is $1$ if $h_t(x_i)\neq y_i$ and $0$ otherwise
3. compute the learner's weight
	- each weak learner is given a weight based on its performance
		- high weight is a good learner
		- low weight is a bad learner
	- weight $\alpha_t$ is calculated as $\alpha_t=\frac 12 \ln(\frac{1-\varepsilon_t}{\varepsilon_t})$ 
		- low $\varepsilon_t$, hight $\alpha_t$ 
4. update weights
	- weights updated after training the weak learner: $W_i \leftarrow \frac{w_i}{\sum_{j=1}^n w_j}$ 
5. repeat
	- repeat for specified number of iterations $T$, or until the error becomes small enough
6. Final Hypothesis
	- strong classifier is a weighted sum of all the weak classifiers: $\boldsymbol{H}(x)=sign(\sum_{t=1}^T\alpha_t \cdot h_t(x))$. 
![[Screenshot 2024-10-08 at 13.38.50.png|200]]
![[Screenshot 2024-10-08 at 13.39.47.png|500]]
## Non-Maximum Suppression (NMS)
- a post-processing step to remove redundant detections
![[Screenshot 2024-10-08 at 13.41.05.png|400]]
1. filter bounding boxes by probability
2. sort bounding boxes by probability
3. non-maximum suppression loop
	1. select box with highest score
	2. suppress overlapping boxes
		- compute the Intersection over Union (IoU) between the selected box and all other boxes: $IoU=\frac {Area \; of \; Overlap}{Area \; of \; Union}$
		- if $IoU$ is greater than threshold then boxes overlap too much and the box is likely a redundant detection and so should be suppressed (discarded)
		- if $IoU$ lower than the threshold, box is retained for further consideration
	3. repeat until all boxes have been selected or suppressed
### Performance Considerations
![[Screenshot 2024-10-09 at 10.22.40.png|400]]
**F-score**: $F_1=2\frac{precision \cdot recall}{precision + recall}=\frac{2tp}{2tp+fp+fn}$
- used to evaluate the performance of a classifier, based off precision and recall
## Receiver Operating Characteristic (ROC) Curve
![[Screenshot 2024-10-09 at 10.26.38.png|300]]
![[Screenshot 2024-10-09 at 10.27.46.png|300]]
- aim is to find the point furthest positive point from the $y=x$ line to be used as the threshold for discarding detections