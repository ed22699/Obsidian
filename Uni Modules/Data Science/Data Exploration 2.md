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