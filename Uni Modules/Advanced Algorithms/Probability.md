---
tags:
  - Lesson
  - probability
---
- **Sample space** $S$ is the set of outcomes of an experiment
	- e.g. $S = \{1,2,3,4,5,6\}$ 
- For $x \in S$, the probability of $x$ is a real number between $[0,1]$ s.t. $\sum_{x \in S}P(x) = 1$ 
- sample space is not necessarily finite
	- e.g. flip a coin until first heads shows up $S=\{T, TH,TTH,...\}$ 
	- $P(n)=(\frac{1}{2})^{n}$ where $n$ is the number of flips		
	- $\sum_{n=1}^{\infty}(\frac{1}{2})^{n}=1$ 
- **Event** is a subset $V$ of the sample space $S$ 
	- $P(V) = \sum_{x \in V} P(x)$ 
- **Random variable** $Y$ over sample space $S$ is a function $S \to \real$ 
	- probability of $Y$ taking value $y$ is $P(Y=y) = \sum P(x)$ where $\{x \in S$ $st.$ $Y(x) - y \}$
	- example 

| S   | Y   |
| --- | --- |
| HH  | 2   |
- **Expected value** (the mean) of $Y$, denoted $\expected(Y)$, is $\expected(Y) = \sum_{x \in S}Y(x)\dot P()$ -------
