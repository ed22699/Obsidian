---
tags:
  - Lesson
---
## Short-selling
- to *go long* $X$: to buy $X$, expecting the price to rise (a *bullish* position)
- to *go short* $X$: to sell $X$, expecting the price to fall (a *bearish* position)
- Often abbreviated to just long/short, e.g. "I'm short IBM"
![[Screenshot 2025-10-23 at 22.51.21.png|400]]
## Derivative Contracts
- a contract that derives its value from some other asset
	- asset is known as the *underlying*
		- lots of types
- *Future*: contract that will be executed by/on a set delivery date
	- required to be executed
	- when issued specifies the *forward price*
		- on delivery contract is executed at the forward price
	- buyer of a forward is the *long position*, seller is *short position*
- *Option*: contract that may be executed by/on the expiry date
	- confer a right (but not an obligation) to exercise
	- specifies a *strike price* (or strike) aka the *exercise price*
	- options to sell are *puts*, options to buy are *calls*
- both futures and options are *standardised* and *exchange-traded*
	- standardised: size of the contract (n) and delivery/expiry data are pre-specified
	- exchange-traded: traded in a secondary market, on an exchange, like stocks and shares
### Equity Options
- one options contract: right to buy/sell $N$ shares ($N=100$)
- price of option depends on price of underlying, strike, and risk premium
	- strike price: the price at which you can buy/sell underlying on exercise
- expiry: last date on which you can exercise option
	- *American-style* options: exercise can happen any data up to expiry
	- *European-style* options: exercise happens only on expiry data (at maturity)
- option is written/issued by its *seller*, held/exercised by its *buyer*
- option price determined by three factors
	- *intrinsic value*: money received if the option is exercised now
	- *volatility premium*: dependent on underlying's price volatility
	- *time value*: potential risk-free return on money saved wrt buying underlying
- calls
	- right to buy N units of underlying
	- option-holder can buy at strike price
	- if exercised, option-writer (seller) must sell $N$ shares at strike price
	- *in-the-money* (ITM) if the underlying price is greater than the strike price
	- *out-of-the-money* (OTM, underwater) if underlying price is less than strike
	- *at-the-money* if underlying=strike
- puts
	- right to sell N units of underlying
	- option-holder can sell at strike price
	- if exercised, option-writer must buy N shares at strike price
	- *In-the-money* (ITM) if the underlying price is less than the strike price
	- *Out-of-the-money* (OTM, underwater) if underlying price is greater than strike
	- *at-the-money* if underlying=strike
![[Screenshot 2025-10-23 at 23.19.18.png|500]]
![[Screenshot 2025-10-23 at 23.20.01.png|500]]
![[Screenshot 2025-10-23 at 23.23.27.png|500]]
![[Screenshot 2025-10-23 at 23.28.20.png|500]]
![[Screenshot 2025-10-23 at 23.29.24.png|500]]
![[Screenshot 2025-10-23 at 23.30.44.png|500]]
![[Screenshot 2025-10-23 at 23.34.59.png|500]]
![[Screenshot 2025-10-23 at 23.35.28.png|500]]
![[Screenshot 2025-10-23 at 23.35.52.png|500]]
![[Screenshot 2025-10-23 at 23.36.07.png|500]]
![[Screenshot 2025-10-23 at 23.37.06.png|500]]
![[Screenshot 2025-10-23 at 23.37.40.png|500]]
![[Screenshot 2025-10-23 at 23.38.04.png|500]]
![[Screenshot 2025-10-23 at 23.38.37.png|500]]
![[Screenshot 2025-10-23 at 23.39.33.png|500]]
![[Screenshot 2025-10-23 at 23.40.05.png|500]]
- this is just sophisticated betting
## Betting Exchanges
- electronic marketplaces where gambler interact to find someone to take the opposite side of their bet: they "buy" (back) or "sell" (lay) the outcome of an event
	- traditional bookmaker: customer backs event, bookie lays
	- betting exchange
		- all customers can either back or lay
		- buys and sells are displayed in a manner similar to Limit Order Book (LOB)
		- customers can trade bets "in play" while an event is happening, until final outcome
- traditional bookmakers have argued that allowing anonymous customers to lay events encourages corruption: it's easier to throw a race than it is to win it
![[Screenshot 2025-10-23 at 23.49.31.png|500]]
![[Screenshot 2025-10-23 at 23.55.54.png|400]]
![[Screenshot 2025-10-23 at 23.56.06.png|400]]
![[Screenshot 2025-10-23 at 23.57.17.png|500]]
- IEM is one such prediction market