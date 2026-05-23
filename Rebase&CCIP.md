# Rebase Token: 
   Tokens that change their total supply, but keep the price same.

# CCIP

## Bridging : 
The transfer of assets cross chain.

Bridges are centralized and decentralized both. Native bridges means bridges build by the chain themselves just like zksync provides us 

- Source Chain: Chain from which tokens are transferring
- Destination Chain: Chain that will receive the transferred tokens
  
NOTE: If the address of destination chain is EOA it can only receive tokens not data, but
 if it is a smart contract it can receive both data and tokens. (data can say like automatically stake() my tokens when issue on other chain) 

Token pools can be self managed or ccip managed (using CCT cross-chain tokens)
### Types of Bridging:

1. Mint & Burn Mechansism: Here, we burn tokens on source chain and mint on destination chain,
   the total supply of tokens remains same across both chains.
   
2. Lock & Unlock Mechanism: Here, we lock tokens on source chain and Unlock tokens on destination chain,
    need liquidity providers to provide liquidity of tokens for both chains. Also needs a vault to be
    settuped on both chains to lock and unlock tokens 

3. Lock & Mint Mechanism: Here, we lock tokens on source chain and mint wrapped tokens on destination chain,
    example of it is usdc.e

2. Burn & Unlock Mechanism: Here, we burn tokens on source chain and Unlock tokens on destination chain.
   Mostly wrapped tokens are burned , this mechainsm is used when working with wrapped tokens.
    

## Cross-chain Messaging :
The transfer of data i.e messages across chains

## Cross Chain Token (CCT Standard):
The Cross-Chain Token (CCT) standard is a way to make a token exist natively across multiple 
blockchains while keeping one unified supply and secure interoperability.
Instead of random third-party bridges, the token issuer/contract controls the cross-chain behavior.

-  Circle uses CCTP which is a way to move usdc across chains. we can use it in our contracts
    to transfer usdc liquidity across different chains.

```solidity
User
  ↓
Token Pool Contract
  ↓
CCIP Router
  ↓
Chainlink Network verifies message
  ↓
Destination CCIP Router
  ↓
Destination Token Pool
  ↓
Mint / Unlock Tokens
```
