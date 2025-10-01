---
tags:
  - Article
Url: https://research-information.bris.ac.uk/ws/portalfiles/portal/206346498/Full_text_PDF_accepted_author_manuscript_.pdf
---
**Note this is only up to and including section 2.3**
## Introduction
- successful trading in financial markets requires balancing the conflicting objectives
	- finding a counterparty with whom to trade
		- mostly solved by publicly announcing an intention (*an order*) to trade
		- if order is large other traders are likely to react to this information by moving the price in the adverse direction. Market reaction to large order is a *price impact* or *market impact*. Cost to a trader can be severe
			- suggested market impact increases roughly as the square root of order size
		- *publicly exposing intention to trade is costly*
	- attempt not to disclose one's trading interest
		- disguise large orders by salami-slicing them into multiple smaller orders to be submitted at irregular intervals
			- bears risk of market moving away
		- pass the order to a *trusted broker* who will attempt to find a natural counterparty within their network of customers and connections
			- if order remains secret within the network there is no market impact
			- is incentive for broker to cheat. Using *insider information* for their own gains by *front running* customers, or by selling the information to a third party
			- *Dark pool trading* venues emerged to counter the reliance on trusting human intermediaries
				- alternative electronic trading systems that automatically match orders in private with no human observers
				- unlike publicly visible orders entered onto the public limit order book (PLOB) of a major lit exchange (e.g. LSE or NASDAQ) orders entering a dark pool are invisible, remain there until a match occurs and only afterwards are the details of the trade published
				- means large orders can execute with little market impact
				- 11% of stock trading in the US executed on such systems in the first quarter of 2018
### Dark Pool issues
- *operators of dark pools* with full access to system data are trusted not to spy or abuse the information inside
	- only way to guarantee privacy is to ensure nobody, not even system operators can gain access to the information in the system
		- one mechanism is to apply a *multi-party computation (MPC)* technique 
			- internal algorithm data is held in secret-shared form, processed by a set of servers. If ratio (depending on MPC) of servers remains hones then the internal algorithm variables do not leak, privacy is preserved
			- orders entered into system use protocol to convert external user's order into secret shared form
			- MPC used to perform compuation (order matching) on the secret shared data, s.t. no order information is ever in the clear
			- if a financial regulator (e.g. SEC or FCA)