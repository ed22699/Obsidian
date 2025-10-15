---
tags:
  - generative_ai
---
- conditioning with language
	- CLIP learns to understand what an image means in natural language, not just to label it with a class name
![[Screenshot 2025-10-15 at 15.40.29.png|500]]
- Pros
	- zero-shot learning: it can generalise to tasks and datasets it hasn't seen during training
	- multimodal understanding: it can understand the relationships between text and images
	- flexibility: it does not require retraining for different image classification tasks
	- efficient use of data: it can use internet-scale datasets to learn rich visual and textual relationships
- Cons
	- bias and fairness issues: it inherits biases present in the large-scale datasets used to train it (e.g. gender, race, or culture)
	- dependence on textual descriptions: its performance depends heavily on the quality and specificity of those descriptions. If the text descriptions are vague or ambiguous, CLIP may fail to classify or retrieve images accurately
	- limited fine-tuning: unlike models specifically trained and fine-tuned for tasks (e.g. ResNet for image classification), CLIP may not always achieve state-of-the-art performance on tasks where task-specific fine-tuning is critical. Its zero-shot performance can be surpassed by models that are tailored to a specific task with fine-tuned parameters
	- training cost: CLIP was trained on massive computational resources and datasets, which is not feasible for many smaller organisations or researchers. This limits the ability of others to replicate or extend the work in environments with fewer resources