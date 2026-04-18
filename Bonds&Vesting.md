# DEFi_TYPE: Bonds & Vesting

## Bonds:

🔹 Core Idea of DeFi Bonds,
A contractual exchange where users deposit assets (like stablecoins or LP tokens) and receive protocol tokens
  vested over time at a discount

🔹 Simple Example
You deposit:
- $100 worth of USDC

Protocol gives you:
- $110 worth of its token

But:
- You don’t get it instantly
- You receive it gradually over, say, 5 days


## 🔹 Types of Bonds in DeFi

## 1. Stablecoin Bonds:

User deposits:
- USDC / DAI
Gets:
- discounted protocol tokens

## 2. LP Bonds (Liquidity Bonds):

User deposits:
- LP tokens (e.g., ETH/DAI LP)
Protocol:
- takes ownership of liquidity

This is a game changer pattern in DeFi.

## 3. Vesting Bonds
- Tokens are released linearly over time

# Vesting in DeFi means:
You don’t receive all your tokens immediately — you unlock them gradually over time according to a schedule.

🔹 Simple Intuition

Instead of:
“Here are 100 tokens now”

You get:
“Here are 100 tokens, but you can only claim them bit by bit over time”

## 🔹 Core Math (Linear Vesting)

- V(t)=( Tt−t0/T )⋅P

Where:
- P = total tokens
- T = total vesting duration
- t0= start time
- t = current time
