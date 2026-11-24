---
title: 1. Introduction
navigation:
  order: 110
---

# 1. Introduction

Blockchain technology has become one of the most closely watched fields of the modern technological revolution. Its properties — immutable data, decentralization, and transparent transactions — together have the potential to bring revolutionary change to many industries and social systems.

Applications range widely: faster and cheaper international remittances in finance, more transparent real-estate transactions, better traceability in supply chains, and more. Smart contracts make it possible to execute financial transactions automatically or to sell goods automatically when conditions are met, and are expected to enable new business models and services.

Japan Open Chain is a consortium-type public chain that is fully compatible with Ethereum (chain ID 81). It was designed as infrastructure on which companies and individuals can do business with confidence in the web3 field, which is expected to grow dramatically. The chain maintains sufficient decentralization, high security, and stability, and is operated by trusted Japanese companies in compliance with Japanese law.

This whitepaper provides detailed information on Japan Open Chain as next-generation financial infrastructure. In particular, it describes **Proof of Staked Authority (PoSA)**, which JOC migrates to in the Tokyo Hard Fork: its design, the contract suite that implements the Authority layer, the migration path from PoA, the token economics, and the rationale for the key design choices.

## 1.1 History and Evolution of Blockchain Technology

The history of blockchain technology begins with the Bitcoin whitepaper published in 2008 by a person using the pseudonym Satoshi Nakamoto. Bitcoin provided a peer-to-peer electronic cash system with no need for a central authority, and the blockchain technology behind it drew wide attention.

Following Bitcoin's success, many crypto-assets and projects were built on blockchain technology. Among them, Ethereum, launched in 2015, went beyond a currency and introduced "smart contracts" — programs that run freely on the blockchain. This raised blockchain from a distributed database technology to a distributed computing environment and greatly expanded its possibilities.

Since then, blockchain applications have expanded rapidly, and blockchain is being adopted and researched in fintech, healthcare, energy, real estate, logistics, and many other industries. Blockchain technology continues to evolve: from the first generation of Bitcoin, to a second generation with smart contracts and DApps, to a third generation with improved scalability and interoperability.

## 1.2 Background and Purpose of Japan Open Chain

Ethereum's potential is remarkable, but it also has many problems with scalability, usability, and cost. It processes only a few dozen transactions per second on average, and when the network is congested, running a program can cost anywhere from a few hundred to tens of thousands of yen. There are also obstacles to business use, such as finality speed, chain splits from hard forks, and unclear accountability. Japan Open Chain was developed to solve these problems, as a fully Ethereum-compatible blockchain backed by highly trusted Japanese companies.

To reduce cost and improve scalability while staying fully compatible with Ethereum, Japan Open Chain launched with a Proof of Authority (PoA) consensus algorithm. This raised transaction throughput dramatically, to an average of hundreds to thousands per second. To improve legal stability for businesses using blockchain, highly trusted Japanese companies were chosen as its operators (Validators). The result is "Japan Open Chain": fast, inexpensive, and usable by anyone for web3 business with confidence.

With the Tokyo Hard Fork, Japan Open Chain migrates from PoA to **PoSA**. PoSA is a Proof of Stake structurally identical to Ethereum's, plus an Authority layer through which the consortium controls Validator entry. It keeps JOC's defining feature — operation by trusted Japanese companies — while bringing protocol-exposed finality, on-chain accountability through slashing, and Validators who operate with capital at stake ([4.3.2](04-japan-open-chain.md#432-migration-from-proof-of-authority-poa-to-proof-of-staked-authority-posa)).

The blockchain market is expected to grow dramatically alongside AI, and Japan Open Chain, at the center of that market in Japan, will be a key to opening new possibilities in IT and finance. Through this project, we sincerely hope to bring innovation to everyone.
