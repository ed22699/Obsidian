---
tags:
  - backpropagation
---
- under circumstances where very large gradients are being passed through a ReLU unit incoming weights may be changed (for instance towards strong negative values) so that the unit will not receive a signal above zero (ever) again and remains without output or learning contribution for the rest of training. Qualitatively, the following sequence may occur
	$$\begin{multline}\underbrace{g_i^{'l-1}(s_i^{l-1})}_{assumed \; open} \sum _{j=1}^{d(l)} \underbrace{w_{ij}^l}_{say \; pos} \underbrace{\delta _j ^l}_{BIGpos} \Rightarrow \underbrace{\delta_i^{l-1}}_{BIGpos} \\ \Rightarrow \underbrace{\eta f_j^{l-2} \delta _i ^{l-1}}_{BIGpos} \Rightarrow \underbrace{w_{ki}^{l-1}}_{BIGneg} \Rightarrow \underbrace{s_i^{l-1}}_{neg} \\ \Rightarrow \underbrace{f_i^{l-1}=g_i^{l-1}(s_i^{l-1}) = 0}_{zero} \end{multline}
	$$
![[Screenshot 2025-09-27 at 13.29.08.png|400]]