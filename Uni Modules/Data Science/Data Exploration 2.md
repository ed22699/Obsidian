---
tags:
  - Lesson
  - data_exploration
---
## Descriptive vs inferential statistics
- Inferential/inductive:
	- summarise sample
	- based on probability theory
- descriptive:
	- describe or summarise dataset
	- useful for assessing data quality, developing models, general understanding
	- often presented alongside conclusions inferential statistics
- Univariate measures
	- central tendency (mean, median, mode)
	- variability (variance, quartiles, min, max, kurtosis, skewness)
	- graphical/tabular format (histograms)
## Types of variable
- categorical/discrete (qualitative)
	- nominal
	- ordinal: ordered
	- dichotomous: only two categories
- continuous (quantitive)
	- interval: measured along a continuum and numerical value
		- e.g. temperature measured in Celsius or Fahrenheit
	- ratio: added condition that 0 indicates that there is none of that variable
		- e.g. temperate measured in Kelvin
## Central tendency
- mean $\mu = \frac 1 n \sum_{i=1}^n x_i$
	- can be used with both discrete and continuous values
	- particularly susceptible to the influence of outliers
- median
	- middle score 
	- less affected by outliers and skewed data
- mode
	- most frequent value (discrete)
	- highest bar in histogram (continuous)
- two modes may imply it cannot be modelled with a simple gaussian and may require two gaussians
- usually prefer the median over the mean with highly skewed data
![[Screenshot 2025-02-05 at 12.04.14.png|400]]
## Measures of dispersion
- range: max() - min()
	- only depends on 2 values
	- most useful in representing the dispersion of small data sets
- variance $Var(X) = \frac 1 n \sum _{i=1}^n (x_i - \mu)^2$ 
- unbiased variance: $Var(X) = \frac 1 {n-1} \sum _{i=1}^n (x_i -\mu)^2$
	![[Screenshot 2025-02-06 at 10.59.01.png|400]]
- standard deviation $\sigma = \sqrt{Var(X)}$ (positive square root)
- [[quantiles]]
	- cut-points dividing the range of a probability distribution into contiguous intervals with equal probabilities
	- dividing the observations in a sample in the same way
	- there is one less quantile than the number of groups created
## Raw moments
Let $X$ be a random variable with a probability distribution $P$ and mean value $\mu = \mathbb E [X]$ (i.e. the first raw moment or moment about zero), the operator $\mathbb{E}$ denoting the expected value of $X$
### Central moments
- $n^{th}$ central moment: $\mu _n = \mathbb E [(X - \mathbb E [X])^n]$ 
	- $\mu _0 = \mathbb E [(X - \mathbb E [X])^0] = 1$ 
	- $\mu _1 = \mathbb E [(X - \mathbb E [X])^1] = 0$ 
	- $\mu _2 = \mathbb E [(X - \mathbb E [X])^2] = \sigma ^2$ (variance) 
	- the third and fourth central moments are used to define the standardised moment which are used to define skewness and kurtosis, respectively
### Standardised moments
- ratio of the $k^{th}$ moment about the mean and the standard deviation to the power of $k$
	$$\bar{\mu} _k = \frac {\mu _k}{\sigma ^k} = \frac{\mathbb E [(X - \mu)^k]}{(\sqrt{\mathbb E [(X - \mu)^2]})^k}$$
- $\sigma$ is sqrt of 2nd moment raised to power of $k$
- power of $k$ is because moments scale as $x^k \rightarrow$ scale invariant
- advantage is they differ in properties other than variability allowing comparison of shape of different probability distributions
### Cumulants
![[Screenshot 2025-02-06 at 11.17.59.png|500]]
## Measures of shape: skewness
- symmetric distributions (if defined) = 0
$$Skew[X] = \mathbb E [(\frac{X-\mu}{\sigma})^3]=\frac {\mu _3}{\sigma ^3} = \frac {\mathbb E [(X-\mu)^3]}{(\mathbb E [(X-\mu)^2])^{3/2}} = \frac{k_3}{k_n^{3/2}}$$
- where:
	- $\mu _3$: third central moment
	- $k_t$: $t^{th}$ cumulants
- sample skewness:
$$b_1 = \frac{m_3}{s^3} = \frac{\frac 1 n \sum _{i=1}^n (x_i - \bar x)^3}{[\frac 1 {n-1} \sum _{i=1}^n (x_i - \bar x)^2]^{3/2}}$$
- $m_3$ and $s_3$ are sample equivalent of $\mu$ and $\sigma$
![[Screenshot 2025-02-06 at 11.25.41.png|300]]
## Measures of shape: kurtosis
- heaviness of the tail of the distribution, compared to the normal distribution of the same variance
- always positive
- kurtosis of a normal is $3\sigma ^4 \Rightarrow excess \; kurtosis = Kurt[X] - 3$
$$ Kurt[X] = \mathbb E [(\frac {X-\mu} \sigma)^4] = \frac {\mu _4}{\sigma ^ 4} = \frac {\mathbb E [(X-\mu)^4]}{
(\mathbb E [(X-\mu)^2])^{4/2} }$$
- sample excess kurtosis:
$$g_2 = \frac {m_4}{s_4 ^2} - 3 = \frac{\frac 1 n \sum _{i=1}^n (x_i - \bar x)^4}{(\frac 1 {n-1}\sum _{i=1}^n (x_i - \bar x)^2)^{4/2}} - 3$$
![[Screenshot 2025-02-06 at 11.46.04.png|400]]