2025-01-10 22:54
#### Tags: [[quad]]
--- 
Your task is to deploy and work with the ICRC-1 and ICRC-2 token standards on the Internet Computer (ICP) blockchain using Rust. You will perform various transactions, create identities, and track balances and cycle burns.

**Steps**

1. Understand the Standards:


[[ICRC-1 Standard]]: A token standard for fungible tokens on the ICP. This standard specifies the basic functionalities a token must implement.

[[ICRC-2 Standard]]: An extension of ICRC-1 that includes additional features.

Documentation: Review the ICRC-1 documentation and the ICRC-2 documentation to understand the methods and functionalities.

1. Setup and Deployment:

Deploy the ICRC-1 and ICRC-2 standards on the ICP blockchain in your local machine.

Ensure the deployment is successful and the token contracts are operational.

1. Create Identities:

Create five accounts "user1", "user2", "user3", "user4", and "user5".

Additionally, have a 'dev" account (for initial transfers) and a 'minter account (for minting tokens).

1. **Perform Transactions:**
	- Transfer 1,000,000 tokens from the 'dev' account to 'user1", "user2", and "user3", 
	- Transfer 1,000,000 tokens from the 'minter" account to "user4" and "user5".
	- Transfer all tokens from'user5' back to the "minter".
2. **Track Balances and Cycles:**
Keep track of the balance of tokens for each account after each transaction
Monitor if any cycles are burnt during the transactions If cycles are burnt, document the reason. If no cycles are burnt, explain why.

In case you don't understand any keywords or functions in the process, study the documentation, do necessary research and then implement it.


---

## **Observations:**
This a diff after and before a transaction from `user3` to `user4` of `500000` token
```bash
❯ diff before_transfer.txt after_transfer.txt
9c9
< Balance: 99_999_567_401_385 Cycles
---
> Balance: 99_999_566_701_743 Cycles
14,17c14,17
< Number of queries: 24
< Instructions spent in queries: 3_060_348
< Total query request payload size (bytes): 960
< Total query response payload size (bytes): 1_062
---
> Number of queries: 27
> Instructions spent in queries: 3_417_168
> Total query request payload size (bytes): 1_080
> Total query response payload size (bytes): 1_089

```


1. Cycles Burned:
	- Before: 99,999,567,401,385 cycles
	- After: 99,999,566,701,743 cycles
	- Difference: 699,642 cycles were burned

2. Query Statistics Changes:
	- Queries increased by 3 (from 24 to 27)
	- Instructions spent increased by 356,820 (from 3,060,348 to 3,417,168)
	- Request payload size increased by 120 bytes (from 960 to 1,080)
	- Response payload size increased by 27 bytes (from 1,062 to 1,089)


	Cycles were burned due to the _computation cost_, _memory operation_ and _state_updation_
	1. Computation Cost: The 356,820 additional instructions required cycles to execute
	2. Memory Operations: The increase in payload sizes indicates state changes that required memory operations
	3. State Updates: Recording the new token balances in the canister's state consumed cycles


## Reference