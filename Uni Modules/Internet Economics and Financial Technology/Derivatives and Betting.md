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
	- *in-the-money* (ITM) if the underl