---
tags:
  - statistics_excel
---
- values far from the expected value have a very small probability. If the probability is too small, that is, if our sample mean exceeds a critical size, then we assume that our null hypothesis cannot be correct and reject it. 
	- $\alpha$ is the area of the sampling distribution of the rejection area, i.e. the probability of finding a value that is larger than the critical value
	- for undirected hypotheses, our rejection area is on both sides, and so we divide our area $\alpha$ into two halves
![[Screenshot 2025-08-26 at 11.31.59.png|400]]
## The Significance Level $\alpha$
- widely accepted sizes are:
	- $\alpha = 10\%$ resp, $\alpha = 0.1$
	- $\alpha = 5\%$ resp, $\alpha = 0.05$
	- $\alpha = 1\%$ resp, $\alpha = 0.01$
- $\alpha$ is also the error probability with which we falsely reject the null hypothesis
	- the $\alpha$ chosen should take the risk of a false rejection into account, if less severe than a larger $\alpha$ if life or death than a smaller $\alpha$
![[Screenshot 2025-08-26 at 11.37.58.png|400]]
- we might also fail to reject the null hypothesis even though it is false, this it the $\beta$-error
- the $\alpha$-error and $\beta$-error are not independent of each other. If we decrease the area of the $\alpha$-error we increase the area of the $\beta$-error and vice versa
- to determine the $\beta$-error we need to know how to formulate the null hypothesis correctly so that it represents the population, but we do not have this knowledge, otherwise we would not have formulated the null hypothesis as it is. For this reason, in practice we usually work with the $\alpha$-error
![[Screenshot 2025-08-26 at 11.44.17.png|500]]
## Statistically Significant, But also Practically Relevant?
- statistically significant does not automatically mean practically relevant
	- the sample size has a large influence on whether a result becomes statistically significant. If the sample is large enough, every result becomes statistically significant, even very small differences which may be practically completely insignificant
- measures of effect size are standardised numbers that provide information about how string the effect it. A major advantage of calculating this is that the results from different studies can be compared
- commonly used measures of effect size:
	- Bravais-Pearson correlation coefficient
	- r
	- Cohen's d
- an effect size of $r=0.1$ indicates a small effect
- an effect size of $r=0.3$ is a medium effect
- an effect size of $r=0.5$ and larger measures a large effect
## Steps When Performing a Hypothesis Test
1. Formulating the null hypothesis, the alternative hypothesis, and define the significance level
2. determining the test distribution and test statistic
3. determine the critical value and the rejection area
4. calculating the test statistic
5. decision and interpretation
## How do I Choose My Test?
![[Screenshot 2025-08-26 at 12.03.31.png|500]]
