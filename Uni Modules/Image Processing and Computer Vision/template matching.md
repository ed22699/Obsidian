---
tags:
  - object_detection
---
 slides a template over the input image and finding regions where the template best matches the local image content
### Template matching
find the best similarity (or lowest difference) within the defined threshold
#### Maximum
correlation: 
$$
\frac 1 n\sum_{i=1}^n(\frac{y_i-\mu_y}{\sigma_y})(\frac{\hat{y}_i-\mu_{\hat{y}}}{\sigma_{\hat{y}}})
$$
- $y_i$: pixel $i$ in box $y$ in the image, $y$ has the same size as $y$
>[!todo]
what does this $y_i$ definition mean

- $\hat{y}_i$: pixel $i$ in template $\hat{y}$
- $\mu$: mean
- $\sigma$: standard deviation 
![[Screenshot 2024-10-06 at 13.55.24.png|200]]
#### Minimum
mean absolute error: $\frac 1n\sum_{i=1}^n|y_i-\hat{y}_i|$
mean square error: $\frac 1n\sum_{i=1}^n(y_i-\hat{y}_i)^2$
- $n$: total number of pixels in the template box
![[Screenshot 2024-10-06 at 13.55.02.png|200]]