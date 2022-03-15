+++
title = "Economic inside blockchain: How does supply-demand mechanism works in blockchain?"
author = ["Anak Wannaphaschaiyong"]
tags = ["blockchain", "blog"]
draft = false
+++

The idea behind gas is to make user pays for computational resources required to complete a transaction on a blockchain. This mechanism directly influence demands of a user to run the transaction and computation cost of a smart contract. (<a href="#citeproc_bib_item_1">El Faqir El Rhazoui 2021</a>)

To better understand the mechanism.
what is gas limit? high has price = high fee &amp; quick, low gas price = long time &amp; slow or transaction denied. Note that in that case of transaction denied due to low gas limit set by the user, money will be lost.


## What is Gwei? {#what-is-gwei}

the lowest unit of gas price is GWei. 1 ETH = 1 \* \\(10^9\\)  GWei.
price of GWei is 50 and tranactio cost 21,000 GWeit. totoal cost in GWei = \\(50 \times 21,000\\)
Therefore, users must take into account unit price of GWei.

amount of gas X unit price of Gwei (at the execution time.).

Gas cost depends on operation cost which depends on multiple factors including load, store, jump, etc.

GWei is easy for human to calculate.


## what is Wei? {#what-is-wei}

Price of Wei is more complicated to calculated than Wei. It takes in to account transaction's demand.

Wei is easy for computer to calculate.

block gas limit. Each block as a limit unit of gas to be spent on transactions.
block gas limit can be think of as a size of a block."supply" for transaction to be executed.
The bigger the block the harder for miner to mine which result in decreasing network's decentralization.


## Optimizing number of gas supply of blockchain at a given point in time. {#optimizing-number-of-gas-supply-of-blockchain-at-a-given-point-in-time-dot}

Since number of gas available is equivalent of supply, and production of this supplies depends on block size (gas limit per block) and times it take to validate the block (difficulty of the block puzzle.). To maximize number of gas supply, we can adjust difficulties of block puzzle such that (number of block \\(\times\\) size of block) is maximize.

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

It is important to note that HashRate cannot be calculated in real time instead it newly generate per cycle which is about 14 days. Hence, calculation of HashRate lags behind actual supply and demand in the market.


## Footnote {#footnote}

<div class="csl-bib-body">
  <div class="csl-entry"><a id="citeproc_bib_item_1"></a>El Faqir El Rhazoui, Youssef. 2021. “Decentralized Autonomous Organizations on Blockchain: Analysis and Visualization.”</div>
</div>

[^fn:1]: [Factors Affecting Cryptocurrency Mining Profits](https://www.eastshore.xyz/factors-affecting-cryptocurrency-mining-profit/)
