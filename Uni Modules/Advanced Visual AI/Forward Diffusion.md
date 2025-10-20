---
tags:
  - generative_ai_diffusion
---
- *forward* diffusion process that gradually adds noise to input
	- noise schedule options:
		- linear schedule: $\beta_t$ increases from $10^{-4}$ to $0.02$
		- cosine schedule: $\beta_t$ follows a cosine-based progression
	- takes the from of a Markov chain
		- only the most recent point in the trajectory affects what happens next $x_{t+1}$ depends only on $x_t$
		- this is the *Markov Property* and can be formulated as: $P(x_{t+1}|x_t, x_{t-1},...,x_0) = P(x_{t+1}|x_t)$
![[Screenshot 2025-10-20 at 12.26.26.png|400]]
![[Screenshot 2025-10-20 at 12.26.52.png|300]]
![[Screenshot 2025-10-20 at 12.28.50.png|400]]
![[Screenshot 2025-10-20 at 12.34.01.png|300]]
![[Screenshot 2025-10-20 at 12.35.42.png|500]]
![[Screenshot 2025-10-20 at 12.36.58.png|500]]