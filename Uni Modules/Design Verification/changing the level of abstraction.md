---
tags:
  - verification_tools
---
- cut down the number of scheduled events to reduce simulation overhead
	- create larger sections of un-interrupted sequential code
	- use less fine-grained model structure (smaller number of schedulable blocks)
	- use higher-level operators
	- use zero-delay wherever possible
- data abstractions
	- use binary over multi-value bit values
	- use word-level operations over bit-level operations
	 ![[Screenshot 2024-09-24 at 13.34.00.png|400]]
	 ![[Screenshot 2024-09-24 at 13.35.20.png|300]]
	 ![[Screenshot 2024-09-24 at 13.35.51.png|300]]