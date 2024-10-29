---
tags:
  - van_emde_boas_trees
---
- describes an algorithm that divides a problem of size $n$ into $a$ subproblems (of size $\frac n b$) and solves recursively 

Let $a \geq 1$ and $b > 1$ and $f(n)$ is asymptotically positive (function is positive for all sufficiently large $n$),
$T(n)=aT(\frac nb)+f(n)$,
1. if $f(n) =O(n^{log_ba-\epsilon})$ for some constant $\epsilon > 0$, then $T(n)=\Theta(n^{log_ba})$
2. if $f(n)=\Theta(n^{log_ba})$, then $T(n)=\Theta(n^{\log_ba\lg n})$ 
3. if $f(n)=\Omega(n^{log_ba+\epsilon})$ for some constant $\epsilon > 0$, and if $a f(\frac n b)\leq c f(n)$ for some constant $c<1$ and all sufficiently large $n$, then $T(n)=\Theta(f(n))$