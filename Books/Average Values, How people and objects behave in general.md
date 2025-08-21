---
tags:
  - statistics_excel
---
- average values are used to analyse how people and objects behave in general
	- [[#The Arithmetic Mean]]
	- [[#The Median]]
	- [[#The Mode]]
	- [[#The Geometric Mean and Growth Rates]]
## The Arithmetic Mean
$$
\bar{x} = \frac{\sum {x_i}} {n}
$$
- assumes metric data (see [[Statistics Is Fun#Scale]])
- sometimes the data has already been process and are only available in categories
	$$
	\bar x \approx \frac {\sum {\bar x _j \times n_j}}{n}
	$$
	- $\bar x_j$ is the mean value of the respective classes
	- $n_j$ is the number of enterprises in the respective class
	- $n$ is the total number of observed firms
## The Median
- can be used for metric data as well as for ordinal data
## The Mode
- can be used for metric data, ordinal data and nominal data
- you can have more than one mode
## The Geometric Mean and Growth Rates
- calculate average growth rates over time
$$
\bar x_g = \sqrt[n]{x_1 \times x_2 \times ... \times x_n}
$$
	- $\bar x_g$ is the geometric mean or average growth factor
	- $x_i$ are the relative changes from one year to the next, or the growth factors
	- $n$ is the number of growth factors
$$
GF_t = \frac {Y_t}{Y_{t-1}}
$$
$$
GF_t = 1 + \frac{GR_{t,\%}}{100}
$$
	- $GR_{t,\%}$ is the growth rate in percent from time point $t-1$ to $t$
	$$
	GR_{t,\%} = \frac{Y_t - Y_{t-1}}{Y_{t-1}} \times 100\%
	$$
- if we subtract 1 from the average growth factor and multiply this by 100%, we receive the average growth rate of the years
	$$
	\phi GR = (\bar x_g -1) \times 100 \%
	$$
	- $\phi GR$ is the average growth rate
## What average value should we use and what else do we need to know
- scale and what we want to calculate decides this
- arithmetic mean is very sensitive to outliers or extreme values