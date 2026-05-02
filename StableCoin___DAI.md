# DAI White Paper Explained

## Collateralized Dept Position:
CDPs hold collateral assets deposited by a user and permit this user to generate Dai, but
generating also accrues debt. This debt effectively locks the deposited collateral assets
inside the CDP until it is later covered by paying back an equivalent amount of Dai, at which
point the owner can again withdraw their collateral.

### OverCollaterized CDP:
Active CDPs are always collateralized in excess, meaning that the value of the collateral is
higher than the value of the debt.

## The CDP interaction process:

● Step 1: Creating the CDP and depositing collateral
The CDP user first sends a transaction to Maker_contract to create the CDP, and then sends
another transaction to fund it with  amount and type of collateral that will be used
to generate Dai. At this point the CDP is considered collateralized.

● Step 2: Generating Dai from the collateralized CDP
The CDP user then sends a transaction to retrieve the amount of Dai they want from
the CDP, and in return the CDP accrues an equivalent amount of debt, locking them
out of access to the collateral until the outstanding debt is paid.

● Step 3: Paying down the debt and Stability Fee
When the user wants to retrieve their collateral, they have to pay down the debt in the
CDP, plus the Stability fee that continuously accrue on the debt over time. The
Stability Fee can only be paid in MKR token. Once the user sends the requisite Dai and
MKR to the CDP, paying down the debt and Stability Fee, the CDP becomes debt
free.

● Step 4: Withdrawing collateral and closing the CDP
With the Debt and Stability Fee paid down, the CDP user can freely retrieve all or
some of their collateral back to their wallet by sending a transaction to Maker.

## Pooled Ether (might be pETH):
This was a contract used as vault, users deposits ether and in return gets pETH which was on 1:1 ration, 
This pETH was used as collateral to generate DAI, in early stages when Dai supported single Collateral only, 
now dai uses multi-collateral. 

OPTIONAL READ: At first, Pooled Ether (PETH) will be the only collateral type accepted on Maker. Users who
wish to open a CDP and generate Dai during the first phase of the Maker Platform need to
first obtain PETH. This is done instantly and easily on the blockchain by depositing ETH into
a special smart contract that pools the ETH from all users, and gives them corresponding
PETH in return.

IMPORTANT: 
If there is a sudden market crash in ETH, and a CDP ends up containing more debt than the
value of its collateral, the Maker Platform automatically dilutes(Dilution = minting more PETH → selling it to 
cover bad debt → existing PETH holders' share of the pool shrinks) the PETH to recapitalize the
system. This means that the proportional claim of each PETH goes down.

Diluting PETH means minting new PETH tokens, but they are not distributed to anyone freely. Instead:
The newly minted PETH is sold in the market to raise ETH
That ETH is used to cover the bad debt left by the undercollateralized CDP

## Key External Actors
Aside from normal actors like user, these are actors with special responsibilities and permissions. 
### Keepers:
A keeper is an independent (usually automated) actor that is incentivized by profit
opportunities to contribute to decentralized systems. In the context of the Dai Stablecoin
System, keepers participate in the Debt Auctions and Collateral Auctions when CDPs are
liquidated.
Keepers also trade Dai around the Target Price. Keepers sell Dai when the market price is
higher than the Target Price and buy Dai when the market price is below the Target Price to
profit from the expected long-term convergence towards the Target Price.

### Oracles:
The Maker Platform requires real time information about the market price of the assets used
as collateral in CDPs in order to know when to trigger liquidations. The Maker Platform also
needs information about the market price of Dai and its deviation from the Target Price in
order to adjust the Target Rate when the TRFM is engaged.

To protect the system from an attacker who gains control of a majority of the oracles, and
from other forms of collusion, there is a global variable that determines the maximum change
to the value of the price feed permitted by the system. This variable is known as the Price
Feed Sensitivity Parameter.

As an example of how the Price Feed Sensitivity Parameter works, if the Price Feed
Sensitivity Parameter is defined as “5% in 15 minutes”, the price feeds cannot change more
than 5% within one 15 minute period, and changing ~15% would take 45 minutes. This
restriction ensures there is enough time to trigger a global settlement in the event that an
attacker gains control over a majority of the oracles.

### Global Settlers:
Global Settlers are external actors similar to price feed oracles and are the last line of
defense for the Dai Stablecoin System in the event of an attack. The set of global settlers,
selected by MKR voters, have the authority to trigger global settlement. Aside from this
authority, these actors do not have any additional special access or control within the
system.

## MKR and Multi-Collateral Dai:
After the upgrade to Multi-Collateral Dai, MKR will take on a more significant role in the Dai
Stablecoin System by replacing PETH as the the recapitalization resource. When CDPs
become undercollateralized due to market crashes, the MKR supply is automatically diluted
and sold off in order to raise enough funds to recapitalize the system.


## MKR Governance — Summary:
MKR tokens give holders voting power to control how the Maker Platform is run.

How it works:
Anyone can submit a proposal (a smart contract) to change system settings
MKR holders vote on proposals they approve of Whichever proposal has the 
most votes becomes active and gets permission to make changes.

### Two types of proposals:

- Single Action (SAPC) — executes once, makes its change, then self-destructs. Simple but rigid.
  
- Delegating (DPC) — stays active and can make ongoing or recurring changes
  (e.g. weekly parameter updates). More powerful and flexible.


### Why Two types of proposals:
The two types exist because different situations need different levels of control.

- Single Action (SAPC) is for simple, one-time changes"
e.g. "Change the stability fee from 2% to 3%" Once done, it's over. No need
for ongoing access. Safer because it can't be reused or abused after execution


- Delegating (DPC) is for ongoing, complex governance:
e.g. "Every week, automatically adjust risk parameters based on a vote"
Needs permanent root access to keep making changes over time
More powerful but also more risk if something goes wrong

## Automatic Liquidations of risky CDPs:
To ensure there is always enough collateral in the system to cover the value of all
outstanding Debt (according to the Target Price), a CDP can be liquidated if it is deemed to
be too risky. The Maker Platform determines when to liquidate a CDP by comparing the
Liquidation Ratio with the current collateral-to-debt ratio of the CDP.

Each CDP type has its own unique Liquidation Ratio that is controlled by MKR voters and
established based on the risk profile of the particular collateral asset of that CDP type.
Liquidation occurs when a CDP hits its Liquidation Ratio. The Maker Platform will
automatically buy the collateral of the CDP and subsequently sell it off. 

### Liquidity Providing Contract — Simple Summary
When a CDP is liquidated, the system takes it over and sells off the PETH collateral to cover the debt.
In Single-Collateral Dai (SAI), there are no partial liquidations.

Three possible outcomes:

- Exact amount raised — Dai collected is used to wipe the debt. CDP owner gets back remaining collateral minus fees & penalties.
- More than enough raised — Extra Dai is used to buy and burn PETH → PETH becomes more valuable → PETH holders gain
- Not enough raised — System mints and sells more PETH to cover the gap → PETH gets diluted → PETH holders lose value

In plain English:
The system sells collateral to pay off bad debt. If it collects too much, PETH holders benefit. If it falls short, PETH holders pay the price through dilution.

In Single-Collateral Dai (SAI), there are no partial liquidations.
When a CDP gets liquidated:
The entire CDP is liquidated at once
The system takes over the whole position
The user loses control completely
Whatever is left after paying debt + fees + penalty is returned to the owner


## Two types of Auction During Multi-Collateral Liquidation
### Debt Auction 🔴
Purpose: Raise DAI to cover the bad debt

When does it trigger?
When a CDP is undercollateralized and the system needs DAI urgently to cover the shortfall

How it works:
- System mints new MKR tokens
- Bidders compete by offering DAI in exchange for that MKR
- The bidder willing to accept the least MKR for their DAI wins
- This raised DAI is used to cover the CDP's debt

Effect:
MKR supply increases → existing MKR holders get diluted


### Collateral Auction 🟢
Purpose: Sell the CDP's collateral and counteract MKR dilution

When does it trigger?
Runs in parallel with the Debt Auction, immediately after liquidation

How it works — Two Phases:

- Phase 1 — Raise enough DAI:
CDP's collateral is auctioned off for DAI
Bidders compete by offering more and more DAI
All DAI collected is used to buy and burn MKR → reversing the dilution from the Debt Auction

- Phase 2 — Reverse Auction (if enough DAI is raised)

Once debt + liquidation penalty is fully covered, it flips into a reverse auction
Now bidders compete by accepting less and less collateral
Whoever accepts the least collateral wins
Leftover collateral is returned to the original CDP owner


### Side by Side Comparison
"What is Raised" = What money/value is collected from the auction

| Category              | Debt Auction              | Collateral Auction         |
|-----------------------|---------------------------|----------------------------|
| What is sold          | Newly minted MKR          | CDP's collateral           |
| What is raised        | DAI                       | DAI                        |
| Purpose of DAI raised | Cover bad debt            | Buy & burn MKR             |
| Effect on MKR         | Dilutes supply            | Reduces supply             |
| Winner bids           | Least MKR for DAI         | Most DAI for collateral    |
