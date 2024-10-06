---
tags:
  - object_detection
---
- Tesseract OCR
1. uses [[Thresholding methods]] (adaptive thresholding) to convert the image into a binary image 
2. pre-processes the image into a clean word image
	- deskewing (detect lines and straighten)
	- character segmentation (split by character)
	- cleaning (e.g. morphological opening)
3. text recognition to convert the clean word image into text
	- originally tesseract employed feature matching
	- since 2018 now uses neural network system based on long short-term memory (LSTM) has been included