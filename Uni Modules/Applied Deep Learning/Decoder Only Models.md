---
tags:
  - gen_DL
---
## Auto-Regressive Models
- use the previous output as input
![[Screenshot 2025-10-22 at 10.41.49.png|200]]
- originally used for time-series prediction, has been used in generative models
![[Screenshot 2025-10-22 at 10.43.20.png|100]]
- think back to encoders and decoders
	- for generating text we only require a decoder
### Decoder Only Models
- what about prompts?
	- might expect this to need an encoder, but we can just prepend this 
		- remember the auto-regressive nature of these models
- *pros*:
	- wee don't need an encoder
	- use the same generation task
- *cons*:
	- context length now adds more attention
		- scales terribly ($O(n^2)$)
	- can cheat with attention
		- all tokens attent to all tokens
		- this would lead to cheating during training
	![[Screenshot 2025-10-22 at 10.48.06.png|250]]
### Masked Attention
- to prevent cheating, we mask out all the future positions in the attention matrix
	- can be calculated quite efficiently with a lower triangular matrix
		- predicting $w_{n+1}$ becomes easy
![[Screenshot 2025-10-22 at 10.50.01.png|100]]
## How do we train our transformer decoder?
- start with a lot of data
- aim:
	- we want to predict the next token in a sequence
- classification is a discriminative task yet ChatGPT is a generative model because we're predicting the most likely next token
## Beam Search
- after the input prompt has been parsed, we predict the first token
![[Screenshot 2025-10-22 at 10.57.07.png|300]]
- as we continue inference we need to continue predicting words
$$
p(w_1, w_0|x) = P(w_0|x)\cdot P(w_1|w_0, x)
$$
- Ideally, we need to calculate
$$
\arg \max_w \prod_{t=0}^n p(w_t|x, w_{t-1}, ..., w_0)
$$
- Beam search extends breadth first search with a new parameter:
	- Beam Width, $B$
- each stage, keep the top $B$ words and model the joint probability
	- we reduce the number of paths significantly
	- some resilience to multiple branches 
	- need to duplicate the inference $B$ times per token
![[Screenshot 2025-10-22 at 11.03.46.png|400]]
## Instruction Tuning 
- so far given a sequence of text our model will try to generate text that will complete it
	- i.e. won't answer questions
- next step is instruction tuning
	- increases the model's capacity to respond to user inputs
	- example of a fine-tuning step
- the *supervised* portion of training
	- model is trained on input prompt and output pairs
		- `<input> what are the colours in the rainbow`
		- `<output> the colours in the rainbow are: red, orange, yellow, green, blue, indigo, violet`
- this data can be hard to get
	- solution is just to use someone else's model
- at this step, *more tokens* are normally introduces for help with downstream tasks
	- e.g.
		- start of prompt
		- end of prompt
		- image start
		- image end