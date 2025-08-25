---
tags:
  - statistics_excel
---
- secondary data is using data that someone else has collected
- primary data we collect the data specifically for our research question
## The Random Sample: The Best Estimator for Our Population
- when collecting data we must clarify the following
	- who is the population or about whom do we want to make a statement
	- do we conduct a census or a random sampling
	- if we conduct a random sampling, how do we achieve that the sample is representative of the population
	- how large should the sample be
- a sample is a subset of the population
	- the sample must behave in exactly the same way as the population with regard to the subject of the study
	- for this we draw the sample randomly out of the population
$$
E(\bar x) = \mu
$$
- where:
	- $E(\bar x)$ is the value we would expect when drawing a sample
	- $\mu$ is the mean of the population
$$
\hat{\sigma}_{\bar x} = \frac s {\sqrt{n}}
$$
- where 
	- $\hat \sigma _{\bar x}$ is the estimated standard deviation of the sample means, we also refer to this as the standard error of the mean
	- $s = \sqrt{\frac{\sum{(x_i - \bar x)^2}}{n-1}}$ is the standard deviation of the sample
	- $n$ is the number of observations
- from the sample mean and the standard error of the mean, we can calculate the interval in which the true value of the population probably lies. This is the confidence interval
- we usually apply three intervals, the 90%, 95% and 99% confidence interval:
	- $CI_{90\%} = [\bar x - 1.64 \times \hat \sigma _{\bar x}; \bar x + 1.64 \times \hat \sigma _{\bar x}]$
	- $CI_{95\%} = [\bar x - 1.96 \times \hat \sigma _{\bar x}; \bar x + 1.96 \times \hat \sigma _{\bar x}]$
	- $CI_{99\%} = [\bar x - 2.58 \times \hat \sigma _{\bar x}; \bar x + 2.58 \times \hat \sigma _{\bar x}]$
- the confidence interval has a 90% probability of covering the true value of the population
- using the width we can work out the sample size needed
$$
n = \frac{2^2 \times 1.96 ^2 \times s^2}{CIW_{95\%}^2}
$$
- where 
	- $n$ is the sample size
	- $s$ is the standard deviation of the sample
	- $CIW_{95\%}$ is the confidence interval width of the 95% confidence interval
> [!note]
The sample size does not depend on the size of the population

- we can apply the considerations made for the mean value to proportion values
$$
E(p) = \pi
$$
- where 
	- $E(p)$ is the proportion value we expect when drawing the sample
	- $\pi$ is the proportion value of the population
$$
\hat \sigma _p= \sqrt{\frac{p(1-p)} n}
$$
- where 
	- $\hat \sigma _p$ is the standard error of the proportion value
	- $p$ is the proportion value of the sample
$$
n = \frac{2^2 \times 1.96 ^2 \times p(1-p)}{CIW_{95\%}^2}
$$
## Of Truth: Validity and Reliability
- proxy is the technical term for a variable that gives approximate information about the issue in which we are interested
- validity of a variable means that the variable is a good proxy for the object of interest
- reliability means that we measure the object of interest with a measurement error as small as possible