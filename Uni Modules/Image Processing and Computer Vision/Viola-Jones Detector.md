---
tags:
  - Lesson
  - viola_jones_detector
---
is a sliding window detector
Haar-like features:
- is a filter of a white square on a black square, in different orientations, attempting to find the similarities to features of the image (e.g. edges in that direction)
- if hard edge the filter will produce a large number
- soft edge will produce a smaller number 
- no edge will produce a very small number
Integral Image:
- calculating features on top of regions to make it less costly
- same size as input image
- for each value in the integral image its calculating the sum of a region in the original image from point (0,0)
- you can find the total value of a region (useful for Haar-like features) through taking the pixel where it 