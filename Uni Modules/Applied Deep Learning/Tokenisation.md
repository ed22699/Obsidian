---
tags:
  - gen_DL
---
## Words
- initially assign each word an index
- ideally, we want a function that can incorporate information: $e_{w_i}=f(w_i)$
	- as $e_{w_i}$ is a vector, we can use it to calculate distances between words in this space
	- Word2Vec was early approach to this
- given a word the Skip-gram model attempts to predict words before after
	- it is learning information from co-occurrences of words
![[Screenshot 2025-10-22 at 10.30.56.png|200]]
- learned some semantics automatically (not many though)
	- A is to B as C is to D
	- with the power of larger models, this representation is now intrinsically learnt
- *Issues*:
	- Climb, climbing and climbed would be considered completely unique
	- anywhere between 180,000 and 1,000,000 words in English
### Tokenisation
- character encoding was first attempted
	- each character is mapped to a unique token:
		- a: 1, b: 2, ... z: 26, A: 27,...
- small vocabulary but now the model needs to learn how groups of tokens fit together
	- we have to teach the model the nuances of the English language and spelling
#### Byte Pair Encoding
- start with character tokenisation
- merge common tokens
- repeat until a desired vocabulary size is found
![[Screenshot 2025-10-22 at 10.37.46.png|100]]
- tokenisers give the LLM a large amount of power, but with issues
- *issues*:  
	- doesn't actually know what is in each token, if you ask ChatGPT for the amount of r's in a word its answer will be dependent on the split of the tokens used to create the word
		- will need to spin up a python program to figure it out
	- spelling and string processing is inherently difficult
	- maths and number understanding
	- languages that use non-Latin characters suffer