- you are aiming to minimise the cost function
	- this is the same as what happens with neural networks
$$
e^2 = E \{(f-\hat f)^2\}
$$
- the minimum of the error function is given in the frequency domain by the expression
	$$
	F(u,v)=[\frac 1 {H(u,v)}\frac{|H(u,v)|^2}{|H(u,v)|^2 + S_\eta (u,v)/S_f(u,v)}]G(u,v)
	$$
	- where
		- $H(u,v)$: degradation function
		- $H^*(u,v)$: complex conjugate of $H(u,v)$
		- $|H(u,v)|^2 = H^*(u,v)H(u,v)$
		- $S_\eta (u,v) = |N(u,v)|^2 =$ power spectrum of the noise
		- $S_f (u,v) = |F(u,v)|^2 =$ power spectrum of the undegraded image