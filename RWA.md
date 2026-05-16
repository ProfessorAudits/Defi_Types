# Real World Assets (RWA):

### Intro:
 RWA's are basically assests in the real world turned into tokenized crypto tokens. 
 For example: Using Real world tesla stock as collateral to mint rTesla tokens, representing 
 real world tesla tokens in crypto space.

 # Types of RWA:

 1. Synthetic RWA
 -  Using crypto as collateral to mint
 -  Deposits real crypto currency like eth or usdc and mint the
    RWA token eg: rTesla

 2. Backed Asset:
- Off-Chain Collateral Based (more powerful & imp)
- Deposits Tesla stock for example in our paper trading accounts as collateral then use chainlink
  function to check for collateral then, mint the RWA token eg: rTesla

 <img width="1771" height="982" alt="Screenshot from 2026-05-15 20-54-46" src="https://github.com/user-attachments/assets/92d4c408-1fbb-4429-b770-19343988bc1c" />

## Architecture: 
The architecture is pretty much same as stable coins. Just need to use chainlink functions to
check off-chain trading collateral.

we use chainlink functions for this that executes our off chain api calls

