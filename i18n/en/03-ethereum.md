---
title: 3. Ethereum and Its Problems
navigation:
  order: 130
---

# 3. Ethereum and Its Problems

With the boom in NFTs, DeFi, and Web3, blockchain infrastructure such as Ethereum mainnet has attracted attention. But by their nature, permissionless blockchains like Ethereum face several challenges for business use. This chapter explains them.

## 3.1 Ethereum's Technical Approach (PoS)

Ethereum is designed as a "permissionless blockchain": anyone who installs the software and connects to the network can immediately become one of its operators.

A permissionless design lets the blockchain run without depending excessively on any individual or organization, and lets services that do not comply with a country's laws be offered from outside that country. This can be very powerful, especially for protecting assets or systems from authoritarian states.

Ethereum originally used Proof of Work (PoW), the consensus algorithm also used by Bitcoin. PoW requires using computing power to the maximum, and its high power consumption made it environmentally unfriendly.

Ethereum has since moved to a Proof of Stake (PoS) consensus algorithm, which produces blocks with a lower environmental load. Under PoS, anyone who deposits 32 Ether (from several million yen to more than JPY 10 million, depending on the price) can become a Validator (operator).

## 3.2 Ethereum's Challenges

Adopting PoS largely solved the environmental problem, but Ethereum's characteristics leave it with various other problems.

### 3.2.1 Slow Speed

In a permissionless network, many node servers must coordinate through a consensus algorithm such as PoW or PoS, which makes it hard to raise transaction speed. The larger the community, the longer decisions such as specification changes take. Bitcoin handles about 7 transactions per second (7 TPS) for the whole world, and Ethereum about 25 per second on average (calculated from about 2.17 million transactions per day in 2026).

This is far too few to meet global demand. As a solution, the Ethereum community is researching and implementing scalability technologies such as Layer 2 chains and sharding. However, Layer 2 technologies still have issues with decentralization, legal stability, and technical approach, and face many challenges for business use. Sharding took its first step in 2024 with the introduction of blobs (EIP-4844), but full implementation is said to need many more years.

### 3.2.2 High Gas Fees

On Ethereum, every transaction requires a fee called gas, paid in Ether. Because Ethereum cannot process many transactions, traffic concentrates. As users increase, gas prices and the price of Ether rise, and at congested times running a single program on Ethereum has cost from a few hundred yen to sometimes tens of thousands of yen. Upgrades in recent years have greatly lowered fees at normal times, but fees still swing widely with demand and the price of Ether, so businesses find it hard to predict their costs.

There have been times when even a simple use case such as sending a stablecoin cost a few hundred to a few thousand yen per transfer. Minting 50,000 NFTs once cost more than JPY 10 billion.

Rising and unpredictable fees on Ethereum mainnet have thus been one of the obstacles to its use.

### 3.2.3 Finality

Because a permissionless network must coordinate a very large number of nodes, it has a specific problem with finality — the time until a transaction can be considered complete.

A blockchain "confirms" a transaction by approving it and including it in a block. On a permissionless blockchain, however, the time until a block is confirmed is not fixed. This is called "probabilistic finality."

PoS mitigates this to some extent: finality is reached after some waiting. Even so, on Ethereum a transaction takes about 13 minutes to complete fully (to be finalized), and until then it is only probabilistic and may be reverted. This behavior can cause serious problems for full-scale financial transactions.

### 3.2.4 The 51% Attack

Blockchain consensus algorithms are vulnerable to the 51% attack: whoever controls a majority of the network can tamper with transactions or double-spend.

On a PoW blockchain such as Bitcoin, holding 51% of the computing power makes it possible to take over the network. This is considered difficult on large networks, but the risk rises on small ones. PoW also raises concerns about power consumption.

On PoS, such as today's Ethereum, the amount of staked assets matters more than computing power. However, high staking requirements and penalty systems tend to make it difficult for ordinary people to participate.

In practice, on a large PoS network like Ethereum, individual participation is hard, so staking-service companies have proliferated, and their large stakes concentrate power on the network. This runs against blockchain's ideal of decentralization.

When large assets such as stablecoins move on a PoS blockchain and the required stake is relatively small, a large organization or state could intervene, commit more than 51% of the staked funds, and take over the network.

In conclusion, especially when introducing PoS on a small network, the risks of 51% attacks and concentration of power must be considered carefully. How Japan Open Chain addresses them is described in [4.3.2](04-japan-open-chain.md#432-migration-from-proof-of-authority-poa-to-proof-of-staked-authority-posa) and [4.5](04-japan-open-chain.md#45-security).

### 3.2.5 Hard Forks

NFTs are products of blockchain technology, and the most important risk to recognize when handling them is the hard fork.

A hard fork is a specification change that is not backward-compatible. When a hard fork occurs, both chains may continue after the split. Permissionless networks run by many participants find consensus difficult, and both Bitcoin and Ethereum have split several times.

Past hard forks have sometimes benefited token holders, but a hard fork on a chain that issues NFTs is a very large risk: it creates duplicate versions of NFTs, which fundamentally conflicts with the idea that each NFT is unique.

Stablecoins are another asset that cannot be split. There is concern that when a hard fork occurs, the stablecoin issuer's intentions may strongly influence how the chain is run.

### 3.2.6 Legal Uncertainty

In many countries, the legal status of permissionless blockchains is not yet clearly defined. This leaves the legal rights to NFTs and applications, and the protection of data, uncertain. Business in countries with international data-transfer regulations requires particular care when using blockchain.

Solving this requires international norms and legal frameworks for blockchain, clear accountability of operators, and clear data-protection policies.

At present, using a permissionless blockchain may pose significant legal-stability problems for companies.
