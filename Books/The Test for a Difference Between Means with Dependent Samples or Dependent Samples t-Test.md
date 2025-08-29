---
tags:
  - statistics_excel
---
- $H_0: \mu_{pre} - \mu_{post} = 0$
- $H_A: \mu_{pre} - \mu_{post} \neq 0$
## The Test Statistic
$$
t = \frac{\sum d_i}{\sqrt{\frac{n \sum d_i^2 - (\sum d_i)^2}{n-1}}}
$$
- where
	- $d_i$ is the difference before and after the treatment
	- $n$ is the sample size or the number of people or objects observed
- here we are using the test statistic to compare the difference between the pre and post treatment values
## The Effect Size
$$
r = \sqrt{\frac{t^2}{t^2 +df}}
$$
- where
	- $t$ is the t-value of the test statistic
	- $df$ are the degrees of freedom
## Calculating the Dependent Samples t-Test with Excel
- Data Analysis tool under the Data tab provides: t-Test: Paired Two Sample for Means
	- enter both training sets
	- assume zero for the hypothesised mean difference


- In the test for a difference between means in dependent samples, we address the question of whether a treatment has an influence on people or objects.
- In the test for a difference between means in dependent samples, we examine the same people or objects twice, once before and once after the treatment.
- The test assumes that the test variable is metric and normally distributed.
- For a small sample and metric but not normally distributed data and for ordinal data, we use the Wilcoxon test for dependent samples.
