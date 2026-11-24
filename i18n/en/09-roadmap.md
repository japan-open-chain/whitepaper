---
title: 9. Roadmap
navigation:
  order: 190
---

# 9. Roadmap

This chapter describes Japan Open Chain's roadmap in detail. Japan Open Chain has set out a roadmap to evolve through staged hard forks and new features. The timing of each hard fork after the Tokyo Hard Fork is in planning and will be announced once confirmed.

## 9.1 Roadmap Overview

Japan Open Chain evolves through the following five major hard forks:

- **Tokyo Hard Fork (planned September 2026–March 2027)**: migration to PoSA, synchronization with Ethereum "Prague/Electra", aiming for up to 5,000 TPS
- **Osaka Hard Fork (in planning)**: 500 Standard Validators in addition to the 21 Core Validators; staking of up to 50 million JOC
- **Kyoto Hard Fork (in planning)**: stronger quantum-resistant security, Validator decentralization, and disaster resilience
- **Gifu Hard Fork (in planning)**: lower latency using Japanese technologies such as IOWN; decentralized permanent storage layer
- **Beyond Gifu (in planning)**: staged introduction of advanced features such as zkRollup, dynamic governance, and cross-chain bridges

Through these, Japan Open Chain will establish itself as next-generation international financial infrastructure with "world-class performance", "quantum-resistant security", and "innovative governance".

## 9.2 Roadmap Details

### 9.2.1 Tokyo Hard Fork – Japan Open Chain v2 (2026-2027)

The Tokyo Hard Fork migrates JOC from Clique PoA to PoSA, using a beacon chain structurally identical to Ethereum mainnet's PoS, and synchronizes the execution layer with Ethereum mainnet's latest release, "Prague/Electra". This further strengthens compatibility with Ethereum.

In actual operation, by adjusting the gas limit (the per-block processing limit) while taking storage capacity and other factors into account, JOC aims first to raise network performance to up to 5,000 TPS.

Key features:

- Separation of the execution and consensus layers through the Beacon Chain ([4.2](04-japan-open-chain.md#42-network-overview-and-technical-architecture))
- A new governance model through an on-chain Validator registry (the Authority layer) ([4.7](04-japan-open-chain.md#47-authority-layer))
- Aiming to raise performance to up to 5,000 TPS (theoretical 100,000 TPS)

Mirroring Ethereum's own staging, the Tokyo Hard Fork is delivered through four phases:

| Phase | Name | Timing | What activates |
| --- | --- | --- | --- |
| Preparation | — | From September 18, 2026 | Deposit Contract deployed; beacon chain starts alongside PoA (launched on September 18, 2026) |
| Phase 1 | The Merge | Planned November 27, 2026 | Block production transitions from PoA (Clique) to PoS. From then on, JOC blocks are produced by PoS Validators |
| Phase 2 | Shapella | Planned January 2027 | Validator reward withdrawals enabled (Capella): beacon-chain sweeps push rewards into `WithdrawReceiver` contracts |
| Phase 3 | Dencun | Planned February 2027 | Network throughput optimizations (blobs, EIP-4844). Not directly observable to Validator operators |
| Phase 4 | Pectra | Planned March 2027 | EIP-7002 execution-layer exits enabled, both voluntary and forced |

Each phase is announced by the Consortium Owner. Validators update their client configuration to match the new fork epoch ahead of the announced activation. The consensus layer activates the new fork at the configured epoch, so **Validators that have not updated by then will lose sync and must update before they can attest again.**

DApps and end users observe no discontinuity from the migration, except that Japan Blockchain Foundation's public RPC and Explorers pause for about 30 minutes before and about 30 minutes after Phase 1 (The Merge). Transaction submission, RPC endpoints, and the chain ID are unchanged.

With this phase in place, adoption is expected to grow further in fields that need high frequency and high reliability, such as financial transactions in stablecoins and tokenized shares, and large-scale on-chain games.

The name comes from Tokyo, Japan's capital and financial center, which was considered the most fitting.

### 9.2.2 Osaka Hard Fork – Japan Open Chain v3

This hard fork introduces a mechanism through which 500 Standard Validators can participate in addition to the 21 Core Validators. It makes the blockchain's operation more decentralized while keeping governance easy to steer through the Core Validators, so the chain becomes safer and more secure.

Key features:

- Decentralization through multi-tier Validators (Core 21, Standard 500)
- Entry of domestic and overseas Validators through NFT certification plus staking
- A staking capacity of up to 50 million JOC through a deposit of 100,000 JOC (planned)

Standard Validators are approved after review by the Consortium Owner, through a certification NFT issued to organizations that meet certain conditions and a stake of at least a certain amount of JOC.

After this hard fork, Validators from outside Japan can join, not only the domestic Core Validators, greatly improving the network's decentralization and fault tolerance. In addition, a fee-sharing model will expand staking demand and increase potential demand from JOC COIN investors. Because Core Validators, who vote on major decisions, are limited to Japanese companies, Japan's political and economic stability continues to underpin the chain's governance.

The name comes from Osaka, where the 2025 World Expo brought pavilions from around the world to Japan, evoking a future in which Validators from around the world take part.

### 9.2.3 Kyoto Hard Fork – Japan Open Chain v4

This hard fork advances the design for "a chain that lasts 1,000 years", a goal Japan Open Chain has long held, to carry data across generations.

To that end, drawing on research in the Ethereum community on quantum resistance, it begins serious work on resistance to quantum computers. At the same time, it further decentralizes the Validator community's operation and the geographic distribution of servers within Japan, aiming for a network that is robust in disasters.

Key features:

- Full-scale introduction of quantum resistance
- Further decentralization of Validator community operation
- Stronger geographic distribution of servers within Japan

With security that can withstand the post-quantum era, long-held assets and nationally important data can be preserved safely. This will accelerate adoption in tightly regulated fields such as government and financial institutions, and make the chain easier to use for users who value reliability.

The name comes from Kyoto, Japan's ancient capital, "a capital that has lasted over 1,000 years".

### 9.2.4 Gifu Hard Fork – Japan Open Chain v5

This hard fork reduces consensus-layer latency by introducing high-speed networks using Japanese technologies such as NTT's IOWN, and decentralizes the permanent storage layer using disaster-resistant and politically and geographically stable locations in Japan and abroad.

Key features:

- Lower consensus-layer latency; high-speed network infrastructure
- Redundant permanent storage layer
- Beacon redundancy across multiple sites such as Japan and Switzerland; L2 optimization

By achieving very low latency and high availability even at edge endpoints, it can fully support use cases where latency is critical, such as high-frequency trading, IoT device communication, and real-time experiences in the metaverse. These performance gains will greatly improve the user experience and drive use across the ecosystem.

The name comes from Gifu, a destination very popular with overseas visitors, with geologically strong bedrock and important Japanese scientific facilities such as neutrino detectors.

### 9.2.5 Beyond Gifu

Plans beyond that are still highly uncertain, but we will continue, at a pace of about once a year, to drive technical and operational improvements and innovation in interoperability, scalability, and governance.

Expected hard forks:

- Sapporo v6: native zkRollup, MEV-safe design, stronger privacy
- Nagoya v7: delegated staking, dynamic governance, AI-assisted voting
- Fukuoka v8: trust-minimized cross-chain bridges (IBC/XCM)

*Plans are subject to change.

## 9.3 Renaming the Native Token (JOC COIN)

On September 1, 2025, as part of a brand strategy to raise the ecosystem's international recognition, the native token long known as "Japan Open Chain Token" was renamed to the easier-to-say "JOC COIN". The new name is more intuitive and memorable for developers, users, and investors; the word "COIN" makes its position as a means of payment, an asset, and an investment clear; and removing the geographic element will further accelerate its penetration into global markets, as with Bitcoin, which is increasingly held as a strategic reserve.

## 9.4 Development Roadmap

Japan Open Chain will invest in technical research for the advancement of blockchain and web3 technology.

### 9.4.1 Technical Research

- **Protocol improvements:** higher TPS, quantum resistance, greater robustness
- **Tools and applications:** wallet technology and applications for better usability; support for smart accounts such as EIP-4337
- **Interoperability:** stronger links with other blockchains

On top of PoSA, the following directions are also under consideration (they do not commit to a delivery date):

- **Light-client support.** The sync committee already produces light-client-friendly signatures. A dedicated light-client RPC surface would enable mobile and embedded use cases without requiring a full consensus client.
- **DVT (Distributed Validator Technology).** Threshold signing across multiple operator-controlled machines would reduce single-machine availability risk. The `WithdrawReceiver` model is DVT-compatible: a Validator's signing keys can be split without changing the on-chain accounting.
- **Restaking primitives.** The `WithdrawReceiver` contract is a natural integration point for restaking: Validators could opt in to securing additional services with their staked JOC.

### 9.4.2 Tool Development

- Adoption of tools that leverage Ethereum compatibility
- Development of wallets, authentication methods, and NFT management tools for mass adoption of web3 solutions

## 9.5 Project Roadmap

We plan to advance projects with many companies and web3 businesses to develop Japan Open Chain.

### 9.5.1 Stablecoin Issuance

- Proof-of-concept trials of stablecoins denominated in Japanese yen and foreign currencies are under way with Kiraboshi Bank, Minna Bank, Shikoku Bank, and other financial institutions
- Trials will also proceed with businesses that want to use stablecoins for cheaper fees and instant settlement, in web3 payments such as NFT sales and in existing payments
- This will create an environment in which companies can easily enter web3 business, for example by buying and selling NFTs without going through crypto-assets

### 9.5.2 Expanding Alliance Partners

- Partnerships with and listings on crypto-asset exchanges
- Stronger cooperation with global node providers and NFT marketplaces
- Collaboration with cross-chain protocols
- Collaboration with NFT and DeFi partners

### 9.5.3 Operating Phases

- **Phases 0–2: Launch phases** — network development, testnet operation, mainnet launch, and so on. These phases are complete.
- **Phase 3: Public phase**
  - Goal: make the chain easy for the general public to use
  - Approach: open endpoints to the public, expand node providers and the ecosystem, and add liquidity to the fee token, to grow the user base.
- **Phase 4 onward**
  - Goal: grow the ecosystem's scale and decentralization, and improve the robustness and stability of the network
  - Approach: partner with web3 application providers worldwide, develop tools for usability, conduct R&D for network stability and robustness, strengthen governance, and more.

## 9.6 Outlook

With "full Ethereum compatibility × trust from Japan" as its strength, Japan Open Chain aims to become the world-standard next-generation financial infrastructure by 2030. By combining robust operation by Japanese companies with advanced technology, we will build a safe, secure, and sustainable global chain.
