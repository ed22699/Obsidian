---
tags:
  - statistics_excel
---
- aim to explain the effect of a variable $X$ on the variable $Y$ and what happens to variable $Y$ when the variable $X$ is changed
## The Linear Regression Line and the Ordinary Least Squares Method
- start with a scatter plot, the simple linear regression is to put the optimal straight line through the point cloud, assumes linear relationship
- using the ordinary least squares method, we minimise the distance between our observations and the straight line
$$
\hat Y = b_0 + b_1 X
$$
- where
	- $\hat Y$ are the estimated $Y$-values
	- $b_0$ is the intercept
	- $b_1$ is the slope
- aim is to minimise the sum of the deviations
$$
e_i = y_i - \hat y_i
$$
- where
	- $e_i$ is the deviation between observed and estimated values
$$
\sum e_i = \sum (y_i - (b_0 + b_1 x_i))
$$
- we square them so all are positive
$$
\sum e_i^2 = \sum (y_i - (b_0 + b_1 x_i))^2 \rightarrow min
$$
$$
b_0 = \frac{\sum x_i^2 \sum y_i - \sum x_i \sum x_i y_i}{n\sum x_i^2 - (\sum x_i)^2}
$$
$$
b_1 = \frac{n\sum x_i y_i - \sum x_i \sum y_i}{n\sum x_i^2-(\sum x_i)^2}
$$
## How Much do We Explain, the $R^2$
- $R^2$ determines the power of the regression line 
$$
R^2 = 1-\frac{unexplained \; variance}{total \; variance} = 1 - \frac{\sum (y_i - \hat y_i)^2}{\sum(y_i - \bar y)^2}
$$
- goes between 0 and 1
## Calculating Simple Linear Regression with Excel