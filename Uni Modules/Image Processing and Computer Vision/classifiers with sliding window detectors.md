---
tags:
  - object_detection
---
applying image classification on overlapped patches in the image
### Sliding Window Detectors
- image is tested for object presence window-by-window
	- window is 'slided' and 'scaled' throughout the image
	- each resulting window is judged w.r.t. an object model giving a response indicating object presence or absence
	![[Screenshot 2024-10-06 at 13.38.44.png|200]]