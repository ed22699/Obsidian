---
tags:
  - Lesson
---
![[Pasted image 20251210160736.png|500]]
![[Pasted image 20251210160911.png|400]]
- centralised banks also expose customers to risk and to scrutiny
## Bitcoin
- imagine that Amelia earned some bitcoin by doing some coding
- she wants to use some of it to buy a car from Bea
- the following steps take place as they make their transaction
	1. agree the transaction
	2. create the transaction message
	3. sign the transaction message
	4. broadcast the transaction message
	5. verify the transaction message 
	6. success
### 1. Agree the transaction
- agree car is worth £1000, current exchange rate makes that 0.18 Bitcoin
- Amelia has 10 Bitcoin, she knows adding a small fee to her payment makes it more likely to be processed quickly because the fee will be earned by the miner that mines the block that Amelia's transaction is included in
- she is going to spend a fraction of a bitcoin on this fee
- the fee is not necessary but it is an incentive for bitcoin miners
### 2. Create the transaction message
- Amelia creates a message that includes three components
	- a reference to the earlier transaction that paid the 10 bitcoin that she is going to use to pay for the car (input to the transaction)
	- list of addresses of recipients of the payment (Bea's address and Amelia's address, since the transaction pays her the change back) 
	- a list of amounts to pay to the addresses (transaction outputs)
- if the amounts (Bea paid of car) + (Amelia, change back) < 10 the remainder is the fee for a miner
### 3. Sign the transaction message
- Amelia signs the message by encrypting it using her private key
	- everyone else can confirm that the message was made by Amelia as they can use her public key to decrypt it
	- no-one can encrypt a message like Amelia without stealing her private key (no-one else can spend her bitcoin)
	- encryption doesn't keep the message secret but confirms who the message was authored (encrypted) by
		- hard to make easy to recognise
