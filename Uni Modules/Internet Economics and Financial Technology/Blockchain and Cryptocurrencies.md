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
### 4. Broadcast the transaction message
- Amelia broadcasts the encrypted message along with her public key
- she initiates the broadcast by spreading the message to immediate peers in the peer-2-peer network
- before broadcasting it to their peers, they verify the message by checking that it meets many constraints
	- inputs $\geq$ outputs
	- transactions referenced exist in the blockchain
- her transaction is now one of a number of transactions on the network that haven't yet been included in the blockchain
### 5. Mining
- miners compete to be the first to mine a block containing transactions that haven't yet been added to the blockchain
- winner will get to keep the fee from each transaction and also gets to include a payment to themselves in the block
- this payment incentivises the work that the miners carry out
- mining is hard, takes many compute cycles to win the competition
	- is important as proof of work is what keeps the blockchain consistent and reliable
- *What is a block?*
	- each block has a header formed of
		- *timestamp and version number*
		- *hash of the previous block header* (links new blocks into a chain)
		- *merkle root* summarising the new transactions that the block contains (means every block will contain a history of all bitcoin transactions)
		- a *nonce value* chosen by the miner such that when the header is hashed using $SHA256^2$ the resulting 256-bit hash has at least $x$ leading 0s
			- SHA256 hashes any data, D, into an arbitrary 256-bit string S ($SHA256^2$ means its just applied twice)
			- you could add an arbitrary nonce value to the end of D to keep changing this value until $SHA256^2$ gave you a bit string, S, that evaluated to 3
			- if you just want $SHA256^2$ to give you a hash S such that $S<2^{200}$ things are easier, if you're happy with $S<2^250$ it's even easier
	- after the header comes a list of the transactions that are recorded by the block (and summaries in the block's header), including the transaction that pays the miner his fee
![[Pasted image 20251210223528.png|500]]
![[Pasted image 20251210223626.png|500]]
![[Pasted image 20251210223701.png|500]]
![[Pasted image 20251210223915.png|400]]