---
tags:
  - Lesson
  - sequential_data
---
# i.i.d. Data
- Independent and identically distributed data
	- up to now, we have considered the data points in our dataset to be i.i.d. data
	- **independent**: value of one data point does not affect the others, $p(\boldsymbol{x}_1, \boldsymbol{x}_2)=p(\boldsymbol{x}_1)p(\boldsymbol{x}_2)$
	- **identically distributed**: all data points have the same distribution, $p(\boldsymbol{x}_i)=p(\boldsymbol{x}_j), \forall i, \forall j$
- this means once you have trained a classifier or regressor, you can predict the output for each data point independently
# Sequential Data
- i.i.d. assumption ignores any ordering of the data points
	- data points often occur in a sequence, such as words in a sentence, frames in a video, sensor observations over time, stock prices... (this can be generalised to more than one dimension: object in different parts of an image)
- we cannot model sequential relationships by simply making time or position in the sequence another feature as timestamp or positional index is not in itself an informative feature
- however, the data observed at other points in the sequence tells us about our current data point
	- e.g. you can guess missing words based off the word right before it
	- we can model these dependencies with a [[Markov Chain]]
>[!note]
[[Markov Chain]] in Bayesian statistics we used the chain to sample to find the correct distribution, however, here we are assuming the data is a Markov chain, todays weather will help predict tomorrows weather

## State Space Models
- if we don't directly observe the states we want to model e.g. if we want to predict the state of the weather we can observe the noisy measurements of temperature, wind, rainfall over a period of time
- encounter same problem as we do in i.i.d. classification and regression: sequential variable we wish to predict is not directly observed
- **solution**: State Space Models
	- introduce latent variables, $\boldsymbol{z}_n$ that form a [[Markov Chain]]
		- each observation $\boldsymbol{x}_n$ depends on $\boldsymbol{z}_n$
			- this means we do not need to model the dependencies between observations $\boldsymbol{x}_n$ directly
		- latent variables model the state of the system, while observations may be of different types, contain noise...
		![[Screenshot 2024-10-28 at 10.38.20.png|150]]
	- **Hidden Markov Models (HMMs)**: discrete state $z$, observations may be continuous or discrete according to any distribution
	- **Linear Dynamical Systems (LDS)**: continuous state $z$, observations are continuous, both have Gaussian distributions
	- we will consider both supervised and unsupervised settings
		- $Z$ values are typically hidden from us so unsupervised is more common
### Hidden Markov Models (HMMs)
![[Hidden Markov Models (HMMs)]]

