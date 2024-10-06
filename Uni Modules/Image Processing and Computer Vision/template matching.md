---
tags:
  - object_detection
---
using sliding a template over the input image and finding regions where the template best matches thee local image content
### Sliding Window Detectors
- image is tested for object presence window-by-window
	- window is 'slided' and 'scaled' throughout the image
	- each resulting window is judged w.r.t. an object odel giving a response indicating object presence or absence