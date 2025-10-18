---
tags:
  - Lesson
---
- temporal information is important because a single frame can be ambiguous in what action it shows in the case of visual AI, and a single word can be ambiguous of its intention without the complete sentence
- sequences
	- words: a word
	- audio: a frequency
	- video: an image
	- IMU data: a sensor reading
- how to model sequences
	- convolution calculates output over neighbours, and is fixed in size
		- what if our input size isn't fixed
		- what if our sequences are items
![[Screenshot 2025-10-18 at 15.37.33.png|300]]
- if we try above, everything is treats independently
- *ideas*:
	- representation of history - hidden states - RNNs
	- Many-to-many - positional encoding/attention - transformers
## Recurrent Neural Networks (RNNs)
![[Recurrent Neural Networks (RNNs)]]
$\sqrt d$ is good to smooth it a little make the query to key nice