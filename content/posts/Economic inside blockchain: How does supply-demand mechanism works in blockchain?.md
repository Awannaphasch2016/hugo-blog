+++
title = "Economic inside blockchain: How does supply-demand mechanism works in blockchain?"
author = ["Anak Wannaphaschaiyong"]
tags = ["blockchain", "blog"]
draft = false
+++

## Gas and Denominations of coins {#gas-and-denominations-of-coins}

<a id="figure--fig:img"></a>

{{< figure src="/ox-hugo/screenshot_20220315_124959.png" caption="<span class=\"figure-number\">Figure 1: </span>Denominations of Ethers" width="300px" >}}

In this section, we will focus on denominations of Ethers. The goal is to provide more concrete example into denomination of a coin.

If you are familiar with Etherem, we have heard Wei and GWei. These are not the only two denominators of Ethers. List of all denominators of Ether is shown in Fig. <img> which is from Etherem yellow paper (aka. technical white paper). (<a href="#citeproc_bib_item_2">Wood and others 2014</a>)

These denominators are units of gas cost in transaction. When talking about cost of gas, using GWei is more convenience, hence, a more widely use as a unit of gas price. I cannot find any historical reason why GWei is chosen over Wei other than convenience.

Transaction cost can be easily calculated as (amount of gas \\(\times\\) cost per unit of gas.)

Still, It is important to talk about mechanism in which Wei is value.
Wei value is calculated based on demands of transaction and supply of gas. We will discuss more about economy of block later.

The idea behind gas is to make user pays for computational resources required to complete a transaction on a blockchain. This mechanism directly influence demands of a user to run the transaction and computation cost of a smart contract. (<a href="#citeproc_bib_item_1">El Faqir El Rhazoui 2021</a>)


## Optimizing number of gas supply of blockchain at a given point in time. {#optimizing-number-of-gas-supply-of-blockchain-at-a-given-point-in-time-dot}

Since number of gas available is equivalent of supply, and production of supplies depend on block size (gas limit per block) and times it take to validate the block (difficulty of the block puzzle.). To maximize number of gas supply, we can adjust difficulties of block puzzle such that (number of block \\(\times\\) size of block) is maximize.

The level of difficulties also has to take into account mining power per time unit. Therefore, at a given point in time, we are given mining power per time unit and we have to solve for difficulties that maximize number of gas supply. See the problem statement below for clarification.

```nil
Problem statement
-----------------

Given (mining power per time unit),
We must solve for optimal level of (puzzle difficulties) such that (size of block) and (number of blocks) will results in maximum number of gas supplies

Base on the following constraints.
1. More difficult puzzle --implies--> bigger block -> less number of block
2. number of gas supply = block size * number of block
```

Difficulty level has the following formula.&nbsp;[^fn:1]

\begin{equation}
Difficulty\\\_level = HashRate / Constant
\end{equation}

Exactly, HashRate is the "mining power per time unit" we mentioned above.

It is important to note that HashRate cannot be calculated in real time instead it newly generate per cycle which is about 14 days. Hence, calculation of HashRate lags behind actual supply and demand in the market.


## What is the incentive to mine? {#what-is-the-incentive-to-mine}

As we mentioned above that supply of gas controlled by HashRate, but what exactly is the underlying incentives for mining? the answer is coins as minnig's reward. For every time block puzzle is solved,  fixed number of "reward" is given to miner in the form of coins.

To sum up, solving a block puzzle generate reward to the miner as in the form of coins and these same coins (such as bitcoin) are added to the economy as supply of blocks that contains gas. Furthermore, the coins itself is an asset which contain value and are tradable and whose value is controlled by "coins market".


## Blockchain economy: Economy of computation vs Economy of coins {#blockchain-economy-economy-of-computation-vs-economy-of-coins}

In my understanding, there are two different markets which I called "coin market" (economy of computation) and "computation market." (economy of coins)

I have discussed above about how mechanism of both market works together, but it may not be clear to you. So I have a dedicated section to clarify the distinction between the two markets.

"Computation market" is the market that involves miner, smart contract, and gas. Miners supplies gas by solving puzzle (aka mining). Smart contract can be think of as demand in the market because number gas must be paid as a cost to compute these smart contracts. Lastly, gas is the entity whose value is calculated as (price of Gwei \\(\times\\) number of Gwei) and is used to value cost of transaction.

"Coin market" is the market that involves coins owner (which may or may not be miners themselves, coins buyer, and coins. Coin owners are those who possess coins. Coins buyers are those who wants to be the future owner of the coins. Lastly, coins is an entity that hold monetary values and can use as transfer of wealth.

So at this point, you might be asking "How are the two markets influence one another?"
The only factor that tight the market together is "incentive of the miner." The only reason that miner mines coins is because the coin can be traded in the "coin market" with "real money". And it just happens that the mined coins are, in facts, consist of blocks which provide supply to the "computation market."


## Footnote {#footnote}

<div class="csl-bib-body">
  <div class="csl-entry"><a id="citeproc_bib_item_1"></a>El Faqir El Rhazoui, Youssef. 2021. “Decentralized Autonomous Organizations on Blockchain: Analysis and Visualization.”</div>
  <div class="csl-entry"><a id="citeproc_bib_item_2"></a>Wood, Gavin, and others. 2014. “Ethereum: A Secure Decentralised Generalised Transaction Ledger.” <i>Ethereum Project Yellow Paper</i> 151 (2014): 1–32.</div>
</div>

[^fn:1]: [Factors Affecting Cryptocurrency Mining Profits](https://www.eastshore.xyz/factors-affecting-cryptocurrency-mining-profit/)
