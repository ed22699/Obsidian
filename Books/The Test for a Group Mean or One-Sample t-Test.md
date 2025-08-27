---
tags:
  - statistics_excel
---
## the Test Distribution and Test Statistic
$$
z = \frac{\bar x - \mu}{\sigma _{\bar x}}
$$
- $z$ is the $z$-value of the standard normal distribution
- $\bar x$ is the sample mean
- $\mu$ is the population mean assumed in the null hypothesis
- $\sigma_{\bar x}$ is the standard deviation of the sampling distribution with $\sigma_{\bar x} = \frac{\sigma}{\sqrt n}$ 
- $\sigma$ is the standard deviation in the population 
- $n$ is the number of observations
## The Critical Value
- we determine the critical value, and thus the rejection area, using the standard normal distribution table
## The $z$-value
- we calculate the $z$-value using the test statistic
- insert the sample mean, the mean from the null hypothesis, and the standard deviation of the sampling distribution
## The Decision
- compare our $z$-value with the critical values and decide whether to reject the null hypothesis
- we can also compute the confidence interval
## The Test When the Standard Deviation in the Population Is Unknown or the Sample Is Small $n \leq 30$
- we tend to have the problem that we do not know the standard deviation in the population. In this case, we substitute in the formula of the standard deviation of the sampling distribution
$$
\sigma_{\bar x} = \frac \sigma {\sqrt n}
$$
- the standard deviation of the population $\sigma$ by the standard deviation of the sample $s$. Thus, the standard deviation of the sampling distribution is recalculated as follows:
$$
\hat \sigma _{\bar x}  = \frac s {\sqrt n}
$$
- where 
	- $\hat \sigma _{\bar x}$ is the estimated standard deviation of the sampling distribution
	- $s$ is the standard deviation of the sample
	- $n$ is the number of observations
- the test distribution is then no longer the standard normal distribution, but the $t$-distribution with $df = n - 1$ degrees of freedom
- a small sample is when the number of observations $n$ is less than or equal to 30, in both cases, the critical values are not taken from the standard normal distribution table but from the $t$-distribution table
- the test value is $t$-distributed and the test statistic is as follows
$$
t = \frac{\bar x - \mu}{\hat \sigma _{\bar x}}
$$
## The Effect Size
- usually used with the one-sample $t$-test in Cohen's $d$
$$
Cohen's \; d = \frac{\bar x -\mu}{s}
$$
- where:
	- $\bar x$ is the arithmetic mean of the sample
	- $\mu$ is the population mean assumed under the null hypothesis
	- $s$ is the standard deviation of the sample
- in literature Cohen's $d$ is interpreted as follows
	- small effect, in the range between 0.2 to < 0.5
	- medium effect, ranges from 0.5 to < 0.8
	- large effect,  $\geq 0.8$
	- note it can also take negative values which would go the other way
## Calculating the One Sample t-Test with Excel
- Excel does not provide a function for the one-sample $t$-test
- we can use NORM.S.DIST to calculate the probability with which our test value occurs
	- enter the value of the test statistic as the $z$-value and 1 under Cumulative
	- we get back the probability of the area left of the test statistic
- accordingly we can use the function T.DIST to calculate the exact probability of our $t$-value to occur when the null hypothesis is correct
	- enter our $t$-value, define the number of degrees of freedom and enter 1 under cumulative
	- we get the probability of the area to the left of the $t$-value