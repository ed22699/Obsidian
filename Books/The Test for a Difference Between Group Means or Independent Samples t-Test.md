---
tags:
  - statistics_excel
---
## The Test Distribution and the Test Statistic
$$
t = \frac{\bar x_1 - \bar x _2}{\hat \sigma_{\bar x_1, \bar x_2}}
$$
- where 
	- $t$ is the t-value of the t-distribution
	- $\bar x_1$ and $\bar x_2$ are the sample means of the respective groups
	- $\hat \sigma_{\bar x_1, \bar x_2}$ is the estimated standard deviation of the sampling distribution
- if we take a closer look at the standard deviation of the sampling distribution
$$
\hat \sigma_{\bar x_1, \bar x_2} = \sqrt{[\frac{(n_1 - 1)s_1^2 + (n_2 - 1)s_2^2}{n_1 + n_2 - 2}][\frac{n_1 + n_2}{n_1 \times n_2}]}
$$
- where
	- $n_1$ and $n_2$ is the number of observations of the respective groups
	- $s_1$ is the standard deviation of the sample of the first group
	- $s_2$ is the standard deviation of the sample of the second group
## The Critical t-Value
- determine using the t-distribution table and the degrees of freedom
## The t-Value and the Decision
- fill in our test statistic with the required values, using the t-value make the test decision
## The Effect Size
$$
r = \sqrt{\frac{t^2}{t^2 + df}}
$$
- where
	- $t$ is the t-value of the test statistic
	- $df$ is the degrees of freedom
- values can be interpreted as follows
	- r smaller $< 0.3$ indicates a small effect
	- r in the range between $0.3$ to $<0.5$ is a medium effect
	- r in the range of $0.5$ to $1.0$ indicates a large effect
	- r cannot be greater than $1.0$ as it is the theoretical maximum
## Equal or Unequal Variances
- excel provides the possibility to compute the test with equal or unequal variances
## Calculating the Independent Samples t-Test with Excel
- the commands for testing difference between group means are available within Data tab and in the Data Analysis tool $\rightarrow$ t-Test: Two-Sample Assuming Equal Variances and t-Test: Two-Sample Assuming Unequal variances


- In the test for a difference between group means, we address the question whether two groups in their population differ with respect to the average behaviour.
- The test assumes that the test variable is metric and normally distributed.
- If the sample is small and the test variable is metric but not normally distributed, or if the test variable is ordinal, we can use the Mann−Whitney test.
- The test for a difference between group means is often called independent samples t-test.
- Depending on whether the variances are equal or unequal, we perform the test for equal variances or unequal variances.