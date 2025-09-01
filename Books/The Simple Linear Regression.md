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
\sum e_i^2 = \sum (y_i - (b_0 + b_1 x_i))^2 \rightarrow min!
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
- two options
	- use excel to draw a scatter plot and then display both the formula of the regression line and the coefficient of determination in the scatter plot
		- when we use the scatter plot a large plus sign appears, offers Trendline, this gives the option to add a linear line
		- select linear and the least squares line is displayed in the scatterplot
		- click more options and check display equation on chart and display R-squared value on chart
	- use INTERCEPT, SLOPE and RSQ 
## Is One Independent Variable Enough, Out-of-Sample Predictions, and Even More Warnings
- we usually have several independent variables that may influence the dependent variable. 
	- we must include all relevant variables in the regression model. If we do not do this, we may overestimate the influence of the included independent variable and our forecasts will be inaccurate
- we should normally only make them in the range of our observations
	- predictions outside our observation range assumes that the relationship found holds beyond the observed range
- linear regression is inadequate when it is not a linear relationship
