---
tags:
  - freq_domain_and_trans
---

## Fast filtering using the Convolution theorem
![[Screenshot 2024-09-27 at 08.17.26.png|400]]
## Ideal Low Pass Filter
 ![[Screenshot 2024-09-27 at 08.23.34.png|400]]
 - filter applied to the FS: $H(u,v)=\begin{cases}1 & r(u,v)\leq r_{0}\\0 & r(u,v)>r_{0}\end{cases}$
	 - $r(u,v)=\sqrt{u^{2}+v^{2}}$, $r_{0}$ is the filter radius
- **NOTE**: this filter with the abrupt edges causes some strange squirly lines within the image
## Butterworth's Low Pass Filter
![[Screenshot 2024-09-27 at 08.23.05.png|400]]
- solution to the ideal low pass filters squirly lines - remove these abrupt edges caused by the filter by having a different, less strict filter:
	- $H(u,v)=\frac{1}{1+[r(u,v)/r_{0}]^{2n}}$ of order $n$
## Butterworth's High Pass Filter
![[Screenshot 2024-09-27 at 08.32.39.png|400]]
## Other filters
![[Screenshot 2024-09-27 at 08.34.48.png|400]]