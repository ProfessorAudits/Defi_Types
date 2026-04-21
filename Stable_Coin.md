# DEFI_TYPE: STABLE_COIN

## What is a Stable Coin: 
Its simply a coin that is pegged(on 1:1 ratio) to another currency, allowing its price to remain stable, enabling people to have 
  a more buying power.

## 3 Fundamental Functions of Money:
```solidity
1. Storage of Value :
     It is a way for us to keep the value of that money we have generated.
       for example: buying apples and keeping them is a bad storage value
         because the get rot by the time passes and lose their value.
                    
2. Unit of Account :
     A way to measure how valuable something is, when we go shopping we see prices being listed in
       terms of usd. It is an example of usd being used as a unit of account.Pricing something
         in bitcoin would be a bad idea because bitcoin prices changes a lot and very frequently.
                     
3. Medium of Exchange :
    It is a agreed upon method to transact with each other.Like when we go shopping we
      agree to pay dollars in exchange of the item we are buying.      
```
## Categories of Stable Coin:
  
```solidity
1. Relative Stability(Pegged/Anchored or Floating) :
     floating uses maths and some algorithms to keep the price stable, pegging means binding minting to some underlying collateral

2. Stability Method(Governed or Algorithmic):
     Means who and what is minting and burning the tokens. whether the tokens are
      burning/minting on algorithmic basis or through some governance.
       Here because of poor governance/intentionaly poor it can also be centralized like USDC,USDT

3. Collateral Type(Exogenous or Endogenous):
     If the stable-coin fails,does the underlying collateral also fails if YES: "it's Endogenous" if NO: "it's Exogenous";
      if the USDC fails does the underlying collateral dollar also fails? NO. means that USDC is "Exogenous"
```
<img width="1852" height="968" alt="Screenshot from 2026-04-18 23-41-16" src="https://github.com/user-attachments/assets/e158a8fe-76a7-44dc-b640-c67b13a37ed9" />


## Collateralized Debt Position (CDP):
CDPs hold collateral assets deposited by a user and permit this user to generate Stable_coin. Basically CDP is a position based on collateral, in return can generate/mint stable-coins. 
```solidity 
IMP NOTE :The Minted stable-coins are as debt
```

## Over-Collateralized: 
Meaning the position must hold more collateral than minted_or_borrowed tokens/stable-coins.

```solidity
IMP: A 150% collateral ratio means:
Your collateral must be 1.5× your debt

🔹 The formula for Maximum mintable Stable_Coim:
Debt = Collateral / CR​
Where:
Collateral = $1000
CR = 1.5 (150%)
```
## Collateralization Logic:

🔹 Final Answer
👉 With $1000 collateral, you can mint: ≈ 666 DAI (maximum)

🔴 But don’t do this in practice

Minting the max is risky.
🔹 Why?
If ETH price drops slightly:
```solidity
Example:
Collateral falls from $1000 → $900
Debt = 666
New CR: CR= 900/666 ≈135%

👉 Now you’re below 150% → liquidation risk
```
```solidity
🔹 Safe strategy (what pros do)
Instead of max:
Mint ~$400–500 DAI
Keep CR at 200–250%
```

```solidity
🔹 Intuition
150% = minimum safety line
Above that = safe zone
Below that = liquidation zone
```
SAFER MODEL:
```solidity
$1000 collateral
   ↓
Max mint ≈ 666 DAI (danger zone)
Safer mint ≈ 400–500 DAI
```

## CDP Logic Flow:
### Excerpt From DAI Whitepaper
```solidity
● Step 1: 
Creating the CDP and depositing collateral. The CDP user first sends a transaction to Maker to create the CDP,
 and then sends another transaction to fund it with the amount and type of collateral that will be used
to generate Dai. At this point the CDP is considered collateralized.

● Step 2:
Generating Dai from the collateralized CDP. The CDP user then sends a transaction to retrieve the amount of Dai
they want fromthe CDP, and in return the CDP accrues an equivalent amount of debt, locking them out of access
to the collateral until the outstanding debt is paid.

● Step 3:
Paying down the debt and Stability Fee When the user wants to retrieve their collateral, they have to pay down
the debt in the CDP, plus the Stability fee that continuously accrue on the debt over time. The Stability Fee
can only be paid in MKR. Once the user sends the requisite Dai and MKR to the CDP, paying down the debt and
Stability Fee, the CDP becomes debt free.

● Step 4:
Withdrawing collateral and closing the CDP. With the Debt and Stability Fee paid down, the CDP user can
freely retrieve all or some of their collateral back to their wallet by sending a transaction to Maker.
```

## Health Factor:


Health Factor checks where our position stands, tells how close we are to liquidation,
SHOULD check it after any redemption of collateral OR more borrowing or before other stuff 

```solidity
Formula:
Health Factor = (Total Collateral Value * Weighted Average Liquidation Threshold) / Total Borrow Value
```

```solidity
🔹 3. Why is Health Factor Important?**

- Gives borrowers a clear risk indicator ✅

- Prevents liquidation by allowing early adjustments ⏳

- Used by protocols like Aave & Compound

🔹 4. How to Improve Health Factor?**

- Repay some of your debt (reduces Loan Value 📉).
- Deposit more collateral (increases Collateral Value 📈).
- Use stablecoins as collateral to avoid price fluctuations.
```
# Audit Questions:
1. Is it Pegged or floating? 
2. if (pegged) then to what? USDC, WETH ??
3. what stability Method is used (Governed or Algorithmic)? Governed doesn't mean governance, it means central_entity Like USDC.
4. Allowed collateral types?
5. Collateral Type(Exogenous or Endogenous): If the stable-coin fails,does the underlying collateral also fails if YES: "it's Endogenous" if NO: "it's Exogenous";
6. How mints coin?? CDP?, if yes to cdp then see cdp excerpt from DAI whitepaper
7. Over_Collateralized or Under_Collateralized?
   if Overcollateralized,yes then how much percent? 150%?
   if Under_collateralized,yes then how much threshold of liquidation is allowed?
