---
description: >-
  This is a rough draft paper describing the Mango objectives and tentative
  plans
---

# Litepaper

### **The Mango Vision**

Mango intends to merge the liquidity and usability of CeFi with the permissionless innovation of DeFi at a lower cost to the end user than both currently provide. Towards this goal, Mango offers margin trading and perpetual futures along with decentralized governance to decide the future evolution. In the medium-term, the goal to rival centralized exchanges in trading volume is ambitious, but we see no substantial impediments for Mango Markets. In the long run, we believe a permissionless ecosystem will produce spectacular, outlandish and unpredictable innovations which will overtake centralized finance.

### **Why Mango Markets Will Succeed**

The key ingredients for this vision are low latency, low transaction cost and full decentralization. We believe all three ingredients are necessary for the project to be viable and all three ingredients are finally available on Solana.

#### **Latency**

The Solana blockchain provides block times of roughly one second. Although one second is still noticeable, Solana's intended 400ms latency target approaches the limit of human perception.The obvious benefit of low latency is usability—most people get anxious waiting on the status of their transaction. But while reducing user anxiety is important, there is another, oft-ignored benefit of low latency: better liquidity. Liquidity providers' quote spreads are directly proportional to the time required to change the quote. The longer it takes to change a price quote, the larger the risk of significant market movement to the market maker and the wider his quotes must be. At the current one second latency, we believe the raw bid-ask spread can be competitive with centralized exchanges.

#### **Transaction Costs**

Low transaction costs are arguably the raison d'etre of finance. We believe a financial innovation must lower transaction costs to be a full improvement. Therefore, the cost per transaction on all Mango financial tools will be comparable to or lower than the costs in CeFi. We believe this must be true. Lower costs indicate efficiency and more efficient protocols and tools tend to win in the long run. It is not possible to escape fees—service providers \(e.g. liquidators, insurance fund, developers\) on Mango protocols must be compensated. However, Mango will err on the side of lower fees.

#### **Decentralization**

Trying to achieve competitive latency and cost by centralizing key components \(e.g. the orderbook\) will fail in the long run. Centralizing any component is a security risk and severely harms composability. Ultimately, the centralizer decides how other apps may interact with the centralized component and the centralizer neither has the incentive nor the bandwidth to allow all interested parties to participate in the improvements. As a result, centralizing key components gives up the immense upsides of permissionless innovation. Mango Markets will retain the upside.

#### **No Presales, Decentralized Governance** 

The Mango Token \(MNGO\) will govern the protocol. The vast majority of MNGO will be locked in the DAO treasury to be distributed according to token holder wishes. That being said, our vision is that governance ought to reward the people who provide protocol services \(e.g. liquidity providers, oracles\) and the people who build new protocol services \(e.g. developers, or other contributors\). The commitment to distribute the largest portion of the DAO’s power and wealth to future contributors will encourage the most skilled and ambitious builders to join us. Finally, in accordance with the crypto ethos of transparency and equal access there will be no presale of tokens.

Ultimately, Mango intends to win the long game in financial services. Low latency makes our tools usable. Rock bottom fees makes Mango hard to compete against. Decentralization makes Mango hard to kill through centralized incompetence or malevolence. Open governance that allocates power and wealth liberally to builders, will attract the best people to build and govern the protocol. Finally, the permissionless nature will allow the millions of tiny experiments to take place that yield the life changing innovations. We're motivated and driven to build Mango according to this vision, and we hope you'll join us.

### **Margin Protocol**

#### **Highlights**

* **No fees**
* **Cross margined**
* **Allows limit orders on margin**
* **Margin positions pay interest**
* **Pooled SRM for fee reductions**

#### **Design**

The initial margin protocol adds a borrowing and lending layer on top of the Serum Dex v3. The user owns a margin account which is then associated with a serum dex open orders account for each market in the group. The user may deposit any of the tokens included in the group and its value in the quote currency \(typically USDT\) is calculated using an oracle. This value is then used to determine how much a user may borrow. Since positions gained from margin trading are also treated as deposits, the user may take up to 5x leverage. Mango Markets does not charge any fees.

#### **Risks**

**Negative equity accounts and socialization of losses**

If the price of a user's collateral falls fast enough or the price of the borrowed tokens increases fast enough, the account may fall below 100% collateral ratio without a liquidator taking the position. In this case, funds are pulled from lending pools to bring the account to 101% coll. ratio. These losses are socialized across all lenders which may trigger a liquidation cascade if most lenders are also very close to being liquidated.

**Oracle error**

The Solana Flux Aggregator is also brand new in Solana and may have errors in the code. The centralized exchanges feeding the price may also have errors. Since all oracle price publishers are looking at the same centralized exchanges, price errors will affect all of them. This could trigger bad liquidations.

**Illiquid deposits**

There is a chance the user is not able to withdraw deposits because it's borrowed. This could be a problem for someone who needs liquidity immediately. The same issue applies to positions that are lent out—the user may not be able to close a position if the utilization rate is 100%. However, the protocol guarantees a 100% APY while the user waits to be able to withdraw.

**Smart contract exploit**

The code has been looked over by volunteers, but there has not been a formal audit. While there are bounties offered for responsible disclosure of potential vulnerabilities, there is no guarantee that hackers will choose the bounty over a profitable exploit.

### **Perpetual Futures \(WIP\)**

#### **Highlights**

* **Most liquid perp on Solana**
* **Cross margin with Serum dex to enable easy hedging on spot**
* **Simple and familiar UI**
* **On chain CLOB**
* **Funding rate as a function of mark price and index price. Funding paid continuously**

### **Token Distribution**

After the initial distribution of tokens, only the DAO may distribute more tokens via governance proposals. The intent is for MNGO to be distributed liberally to protocol builders, liquidity providers and project contributors in a fully transparent way.  


**Max Supply: 10,000,000,000**

**Initial Circulating Supply: 2,000,000,000**  


**Creators - 5%**

For the work of creating Mango Markets.  


**Insurance Fund Sale - 5%**

There will be a sale of MNGO that goes directly into the DAO treasury for use as the insurance fund. The insurance fund will pay Mango Perps smart contract in the event extreme volatility causes bankrupt accounts and excess losses in the system. The sale mechanism is described in detail below.  


**Temporary Governance Fund - 10%**

This will be used for governance until full governance mechanisms are launched. The temporary governance fund cannot vote and any unused funds will be returned to the DAO treasury, when governance is implemented. The fund is intentionally chosen to be larger than the creators share as we expect exceptional builders to join Mango soon.  


**DAO - 80%**

These tokens can only be unlocked via token holder governance. We propose that tokens are distributed roughly on a logarithmic supply model similar to Bitcoin but with a halving every two years i.e. 50% of the tokens distributed in the first two years, 75% in the first four years, 87.5% in the first 6 years and so on. The DAO is not bound to follow this proposal. 

### Token Sale 

The token sale contract will have two vaults, one with 500,000,000 MNGO and the other vault with 0 USDC. Over a 24 hour period, any Solana user may deposit or withdraw USDC as they wish. At the end of the sale period, all the MNGO in the vault will be distributed to users according to their share of the USDC vault i.e. the tokens are priced pro rata. In order to give some clarity on the price the buyer will pay, the last one hour of the sale period will be withdraw only. Therefore, during the initial 24 hours, the price may go up or down as deposits and withdraws fluctuate, but during the last hour, the price may only go down. 

Mango developers, including those from the community, will build the smart contracts and the user interface. All the code used will be open source and remain free and open source for future teams to use as they wish.

### **Governance**

The MNGO token is a governance token, first and foremost. Collectively, the token holders have the power to upgrade the protocol as they see fit, only constrained by the checks-and-balances of the DAO. This allows token holders to create incentives to reward participation and drive usage of the protocol.

We consider the COMP governance model to be a gold-standard in the industry and followed it to build out the MNGO governance model. We mainly reworked the initial token distribution, to facilitate a DAO inception that is truly open and adapted it’s mechanics to fit the solana programming model. 

Anybody with 0.1% of MNGO staked can propose a governance action; these are simple or complex sets of actions, such as adding support for a new asset, changing an asset’s collateral factor, changing a market’s interest rate model, or changing any other parameter or variable of the protocol that the current administrator can modify.

Proposals are executable code, not suggestions for a team or foundation to implement. They are not limited to the governance protocol itself, but extend to all protocols created by the MNGO DAO including the Margin and Perp protocols contributed by the creators at launch.

All proposals are subject to a 3 day voting period, and any MNGO staker can vote for or against the proposal. If a majority, and at least 2% of the total MNGO supply are cast for the proposal, it is queued in the Timelock, and can be implemented after 2 days.

One thing to note is that before the on-chain governance voting platform is ready for MNGO token holders, core protocol contributors will make critical decisions based on the project vision and informal input from the community on discord. This is intentional, as we think it’s important to keep governance nimble in the early days of the protocol.  


## **Project Status & Roadmap**

#### **Mango Margin "closed alpha"**

* first weeks of march
* enforces strict borrow limits for every account
* liquidator and solana program remain closed source
* 3rd party liquidators begin implementing their strategies

#### **Mango Margin "public beta"**

* begins mid-march 2021 and runs for multiple months
* borrow limits will be replaced with the introduction of partial liquidations
* margin trading interface largely improved based on feedback during alpha phase
* additional trading pairs will be released
* step-wise open source releases as independent reviews are finishing

#### **Mango Perp "closed alpha"**

* Begins early June 2021 and runs for a few weeks
* Market makers can integrate and test

#### **Mango Perp "public beta"**

* Sale of tokens that go directly into insurance fund
* introduces governance token

#### **Mango DAO Launch**

* Formal on-chain governance mechanism
* Website and forums for participation in governance
* Further proposals to reward contributors

\*\*\*\*
