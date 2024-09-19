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
- **Random variable** $Y$ over sample space $S$ is a function $S \to \mathbb{R}$ 
	- probability of $Y$ taking value $y$ is $P(Y=y) = \sum P(x)$ where $\{x \in S$ $st.$ $Y(x) - y \}$
	- example 

| S   | Y   |
| --- | --- |
| HH  | 2   |
| HT  | 1   |
| TH  | 5   |
| TT  | 2   |
$P(Y=2)=\sum_{x \in \{HH, TT\}}P(x) = \frac{1}{4}+\frac{1}{4}$

- **Expected value** (the mean) of a random variable $Y$, denoted $\mathbb{E}(Y)$, is $\mathbb{E}(Y) = \sum_{x \in S}Y(x)\cdot P()$ 
	- example $\mathbb{E}(Y)=(2\cdot \frac{1}{2})+(1 \cdot \frac{1}{4}) + (5\cdot \frac{1}{4}) = \frac{5}{2}$
![[Linearity of expectation]]
# Indicator random variables
- a r.v. that can only be $0$ or $1$
- $\mathbb{E}(I)=P(I=1)$
- often an indicator r.v. is associated with an event such that $I=1$ if the event happens and $I=0$ otherwise
- works well with [[Linearity of expectation]]


![[Markov's Inequality]]

![[Union bound]]