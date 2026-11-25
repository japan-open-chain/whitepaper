---
title: 4. About Japan Open Chain
navigation:
  order: 140
---

# 4. About Japan Open Chain

To solve the problems above, Japan Open Chain was developed as Ethereum-compatible blockchain infrastructure on which Web3 business can be done safely and securely. It is designed as a consortium-type public chain operated by trusted Japanese companies in compliance with Japanese law, with sufficient speed and decentralization and high security and stability.

## 4.1 Concept and Purpose

Japan Open Chain is an Ethereum-compatible, consortium-type public chain that any user in the world can use. It is fully compatible with Ethereum and adopts Proof of Staked Authority (PoSA), under which the consortium controls Validator entry.

JOC launched with Proof of Authority (PoA) and achieved much faster transaction speeds than Ethereum mainnet. Under PoA, who the Validators are is what matters. Japan Open Chain addressed PoA's weakness by having major Japanese companies with high social trust act as Validators. Its Validators are trustworthy Japanese companies, including listed companies.

PoSA keeps this operation by trusted Japanese companies while adopting the same Proof of Stake mechanism as Ethereum. Each Validator puts up stake, and the protocol holds misbehaving Validators accountable through slashing.

Japan Open Chain is thus positioned as an Ethereum-compatible blockchain that balances real business needs against technical challenges, and that assumes operation in Japan, with its political and legal stability.

## 4.2 Network Overview and Technical Architecture

Japan Open Chain runs a blockchain network based on widely used open-source Ethereum node software. Users can easily connect through interfaces offered by node providers and RPC endpoint providers. Because it supports the standard Ethereum JSON-RPC API, existing Ethereum tools and libraries work as they are. How to send transactions, the RPC endpoints, and the chain ID do not change across the Tokyo Hard Fork.

JOC launched on Geth's Clique (PoA). In Clique, a predetermined set of Signers takes turns signing blocks and produces a block every 5 seconds. Japan Blockchain Foundation Inc. regularly audits operations to keep the network healthy and transparent.

From the Tokyo Hard Fork, JOC runs on the two layers below.

### 4.2.1 Two-Layer Structure

| Layer | Made of | Role |
| --- | --- | --- |
| Consensus layer | Ethereum Proof of Stake (the beacon chain) | Selects block proposers, collects attestations (votes on the state of the chain), and handles finality and slashing. It follows the Ethereum specification unchanged; only timing and similar parameters are adjusted to JOC's scale ([4.6](#46-consensus-layer)) |
| Authority layer | Smart contracts on the execution layer | Approves Validator entry, executes deposits, and performs forced exits. Managed by the Consortium Owner, Japan Blockchain Foundation Inc., through a Safe Multisig ([4.7](#47-authority-layer)) |

The only link between the two layers is each Validator's destination for rewards and exit proceeds (its withdrawal credentials). The Authority layer creates a receiving contract (`WithdrawReceiver`) for each Validator and registers its address as that destination. To the consensus layer this is an ordinary address, and it sends rewards and exit proceeds there exactly as Ethereum does. The consensus client (Lighthouse) is therefore unmodified.

### 4.2.2 Node Architecture

After the Tokyo Hard Fork, each Validator's node runs three pieces of software:

| Component | Software | Role |
| --- | --- | --- |
| Execution Client | Geth (Nethermind as an alternate) | Transaction execution, EVM, state |
| Consensus Client | Lighthouse | PoS protocol, fork choice, beacon state |
| Validator Client | Lighthouse VC | Key custody, signing attestations and block proposals |

The execution and consensus clients connect over the **Engine API**, and the Validator Client connects to the consensus client over the **Beacon API**.

The Validator Client runs on servers that each Validator manages itself, and the signing keys never leave those servers. No one other than the Validator can sign with the Validator's keys.

## 4.3 Technical Features

### 4.3.1 Ethereum Compatibility

Ethereum is the blockchain network with the largest user base in the world. Japan Open Chain focuses on compatibility with this vast ecosystem and uses, as they are, "Go Ethereum (Geth)", the most popular Ethereum node software, and "Lighthouse", an Ethereum consensus client. Applications and tools that run on Ethereum therefore run on Japan Open Chain without problems, and software development benefits greatly from the Ethereum community.

Japan Open Chain is essentially part of the Ethereum community, and is registered as Chain ID 81 in Ethereum's chain ID registry (chainlist).

### 4.3.2 Migration from Proof of Authority (PoA) to Proof of Staked Authority (PoSA)

Japan Open Chain is migrating from Clique PoA to the more advanced Proof of Staked Authority (PoSA). The Tokyo Hard Fork (v2) introduces Ethereum's beacon chain technology and manages Validators through smart contracts. The migration is delivered in four phases ([9.2.1](09-roadmap.md#921-tokyo-hard-fork--japan-open-chain-v2-2026-2027)).

**What PoA offered, and why JOC is moving on.** PoA suited the network's launch period: block times were stable, each Validator needed only one client (Geth), and every block signer was an identified Japanese company. After Ethereum moved to PoS, however, PoA (Clique) fell out of Ethereum's official support, and Geth stopped supporting Clique. Staying on PoA was therefore affecting JOC's compatibility with Ethereum, and this is the main reason for the move to PoSA.

**Design goals.** PoSA is designed to meet four goals:

1. **Economic accountability.** Every Validator puts up stake (collateral), and the protocol can automatically confiscate it (slashing) for misbehavior.
2. **Finality.** A finalized block cannot be reverted unless one-third or more of the stake is confiscated.
3. **Consortium control over membership.** Holding JOC alone does not make anyone a Validator; joining requires the consortium's approval.
4. **Ethereum compatibility.** Ethereum software such as Geth, Lighthouse, wallets, and deposit tools works almost as it is.

A permissionless, Ethereum-style PoS meets (1), (2), and (4), but not (3), because anyone with 32 JOC could become a Validator. Continuing with PoA meets (3) but not (1) or (2). PoSA adds a single rule to Ethereum PoS — joining as a Validator requires the consortium's approval. Block production, attestation, fork choice, finality, slashing, and exits all work as in Ethereum.

**Comparison with other chains.** The consensus layer adopts Ethereum PoS as it is, and its slot and epoch lengths follow the settings (preset) of Gnosis Chain, which has a proven record with 5-second blocks. BNB Chain also uses the name "PoSA", but it is a delegated PoS without a beacon chain and works differently from JOC's PoSA.

| Network | Consensus | Validator entry | Stake | Finality |
| --- | --- | --- | --- | --- |
| Ethereum mainnet | PoS | Permissionless (32 ETH) | 32 ETH | Casper FFG (~13 min) |
| Gnosis Chain | PoS | Permissionless (1 GNO) | 1 GNO | Casper FFG (~2.7 min) |
| BNB Chain | "PoSA" (delegated) | Top 45 by delegation (21 Cabinets + 24 Candidates) | Token-weighted | Fast finality (~1 s) |
| Polygon PoS | PoS + checkpoints | Top by stake (active set capped at ~100) | POL | Heimdall checkpoints |
| **JOC PoSA** | **PoS + Authority** | **Consortium approval** | **32 JOC** | **Casper FFG (~2.7 min)** |

**From the Osaka Hard Fork.** The planned Osaka Hard Fork (v3) introduces a three-tier Validator system:

- Core Validators: trustworthy Japanese companies and organizations, including listed companies, that take part in technical and legal governance
- Standard Validators (up to 500 companies): a stake of JOC required (amount to be decided); take part in block production
- Community Validators (unlimited): a stake of JOC required (amount to be decided); take part in network monitoring and governance votes

This tiered approach balances speed and decentralization, and lets more participants contribute to the network while maintaining the reliable finality that the financial industry requires ([4.6.2](#462-fork-choice-and-finality)).

### 4.3.3 Transaction Speed and Scalability

Japan Open Chain raises its transaction throughput step by step as the technology evolves:

- v1 (Clique PoA): thousands of native-token transfers per second; hundreds of smart-contract executions per second
- v2 Tokyo Hard Fork (planned September 2026–March 2027): aiming for up to 5,000 TPS (theoretical 100,000 TPS)
- v3 Osaka Hard Fork (in planning): higher efficiency through multi-tier Validators
- v4 Kyoto Hard Fork (in planning): performance optimization alongside quantum-resistant security
- v5 Gifu Hard Fork (in planning): lower latency using Japanese technologies such as IOWN
- Beyond Gifu (in planning): targeting tens of thousands of transactions per second through native zkRollup integration

Whereas Ethereum itself handles about 25 transactions per second on average ([3.2.1](03-ethereum.md#321-slow-speed)), Japan Open Chain aims to sustain 5,000 TPS. The theoretical figure of 100,000 TPS is based on Nethermind, one of the execution clients JOC uses, reaching about 100,000 transactions per second in a local environment. On a real network, communication and consensus add overhead, so we expect throughput in the tens of thousands of TPS. Because JOC has a small number of Validators, this overhead stays small, which lets JOC handle growth in transactions over the medium to long term.

### 4.3.4 The JOC Crypto-Asset

The native crypto-asset JOC (official name: JOC COIN) is used as the fee token required to operate Japan Open Chain. It also serves as payment for services on the network, as Validator rewards, and, under PoSA, as Validator stake ([6](06-token-economics.md#6-token-economics)). It is not a stablecoin; its price moves with the market. This paper writes the unit as **JOC**.

### 4.3.5 Legal Stability

Japan Open Chain is operated under Japanese law and regulation. This improves legal certainty for companies and individuals doing business and financial transactions. The Validators that produce blocks remain identified Japanese legal entities under PoSA.

## 4.4 Governance Model

### 4.4.1 Progressive Decentralization

Japan Open Chain decentralizes its governance in stages.

**v2 (planned September 2026–March 2027) - Tokyo Hard Fork**

- On-chain Validator management ([4.7](#47-authority-layer))
- Control of the Authority layer by the Consortium Owner's Safe Multisig

**v3 (in planning) - Osaka Hard Fork**

- DAO-NFT certification system (Lv3 = Core, Lv2 = Standard, Lv1 = Community)
- Proposal types: Standard proposals, Fast-Track proposals, Emergency Pause
- Sustainable operation funded by a consortium tax (15–30%)

**v4–v5 (in planning)**

- Fully on-chain promotion and demotion
- Dynamic Governance (thresholds vary by proposal type)
- Delegated Staking & Election model
- Expanding the share of overseas Validators to 30–50%

### 4.4.2 Trust Assumptions

PoSA makes the following assumptions for each of its two layers:

| Layer | Assumption | If the assumption fails |
| --- | --- | --- |
| Consensus layer | Validators holding more than two-thirds of the stake behave correctly (more than half to keep producing blocks) | Blocks may be reverted or the chain may stall (same as Ethereum) |
| Authority layer | The Consortium Owner (Japan Blockchain Foundation Inc., operating a Safe Multisig) uses its authority correctly | New Validators may be refused and existing Validators may be force-exited. If the contract upgrade authority is abused, the flow of funds could be changed |

**Even the Consortium Owner cannot take Validator stake.** All it can do is refuse new Validators or make an existing Validator exit. An exited Validator's stake (less penalties) and its rewards go only to the address the Validator declared at registration, and that address cannot be changed later.

However, the Authority layer contracts can be upgraded, and the property above assumes that the upgrade authority is used correctly. The upgrade authority is held by a Safe Multisig with multiple signers, and the contracts have undergone a third-party security audit.

**PoSA cannot prevent the Consortium Owner from colluding with a majority of Validators.** Such collusion could finalize an invalid state or rewrite history. This assumption is common to all consortium chains, and it is deterred by legal agreements among the participants.

## 4.5 Security

In general, a blockchain is hacked either by exploiting a weakness in its consensus algorithm or by attacking a security hole in the software that supports it. Japan Open Chain's security rests on both its underlying technology and how it is operated.

### 4.5.1 Technical Architecture

Japan Open Chain uses Go Ethereum (Geth) and Nethermind — the most widely used execution clients on Ethereum, tested and improved over many years — as execution clients, and Lighthouse as the consensus client. For the execution client, JOC follows the **multi-client strategy** inherited from PoA: Geth is the default and Nethermind the alternate. Running multiple implementations across the Validator set reduces the risk that a single-client bug halts or forks the network and makes the network more robust. This proven software has withstood many attacks and vulnerability tests.

### 4.5.2 Operating Model

Under PoSA, an attacker must control two-thirds or more of active stake to finalize a chain of its choosing, and more than one-third just to halt finality. On Japan Open Chain, entry to the Validator set is controlled by the consortium, and Validators are operated by companies and organizations with high social trust in Japan. An attacker would therefore have to hack major Japanese companies simultaneously to control a majority of the network. In addition, under PoSA the stake of a Validator that signs maliciously is confiscated through slashing.

Japan Open Chain thus provides sufficient security through both its technical architecture and its operating model.

### 4.5.3 Properties PoSA Guarantees

- **Reverting a finalized block is very costly.** Reverting a finalized block requires one-third or more of the active stake to be slashed. With N Validators, at least ⌈N/3⌉ × 32 JOC of stake is confiscated, plus an extra penalty that grows with the amount of stake that misbehaved at the same time (the correlation penalty).
- **The consortium cannot create fictitious Validators.** Activating a Validator requires a 32 JOC deposit, a signature made with the Validator's own key, and the consortium's approval. The consortium can give approval, but it cannot produce the signature without the Validator's key.
- **The receiving address cannot be swapped.** A Validator's public key is tied to its receiving contract at the first deposit and cannot be changed afterwards. No one can redirect a Validator's funds by sending a deposit that names a different receiver.
- **Damage from a leaked key can be contained.** If an attacker signs conflicting messages with a leaked key, the consensus layer slashes that Validator. The operator can request an exit as soon as it notices the leak. An exit signed with the Validator's key is available at any time from about 5.7 hours after activation ([4.8.3](#483-exit)).
- **The consortium cannot censor individual transactions.** The consortium controls who can be a Validator, not what goes into blocks. Which transactions enter a block is decided by the block proposer chosen for each slot.

The risks the design does not remove are listed in [10.3](10-risks.md#103-residual-design-risks).

## 4.6 Consensus Layer

JOC's consensus layer follows the Ethereum PoS specification ([references 1–7](12-references.md#references)). This section summarizes the main points, focusing on what is specific to JOC.

### 4.6.1 Beacon Chain and Validators

JOC runs a beacon chain alongside its execution chain. It works as in Ethereum, but its timing parameters follow Gnosis Chain's settings:

- A slot (the unit of block production) is **5 seconds**, and an epoch is **16 slots (80 seconds)**.
- One block proposer is chosen at random for each slot.
- Every Validator makes one attestation per epoch.

Validators are identified by BLS12-381 public keys. Each Validator generates its keys in-house and never hands them to anyone else.

### 4.6.2 Fork Choice and Finality

Like Ethereum, JOC combines **LMD-GHOST** (choosing which chain is canonical) and **Casper FFG** (finality). A checkpoint that receives votes from two-thirds or more of the active stake becomes "justified", and once the checkpoint of the next epoch is also justified, it becomes "finalized".

A finalized block cannot be reverted unless one-third or more of the stake is slashed ([4.5.3](#453-properties-posa-guarantees)).

**Finality takes about 2 epochs, or about 2.7 minutes.** This is shorter than Ethereum mainnet's roughly 13 minutes (as of November 2026) because JOC's slots and epochs are shorter.

### 4.6.3 Validator Duties, Rewards, and Penalties

| Duty | Frequency | What it involves |
| --- | --- | --- |
| Attestation | Once per epoch | Vote on the head of the chain and on the finality checkpoints |
| Block proposal | On average once every N slots (N = number of Validators) | Propose a block in the slots where it is chosen |
| Sync committee | Always | Sign blocks so that light clients can verify them |

Because JOC has fewer Validators than the sync committee size (512), every Validator is always in the sync committee. This needs no extra work; the Validator Client handles it automatically.

Rewards are paid with the same formula as Ethereum ([6.5](06-token-economics.md#65-consensus-layer-issuance)). The penalties are:

- **Missed attestations.** A small penalty, small enough to earn back once the Validator is running again.
- **Missed block proposals.** The Validator only misses that slot's reward; there is no extra penalty.
- **Inactivity leak.** If the chain cannot finalize for more than 4 epochs, offline Validators lose stake at an accelerating rate. This mechanism lets finality recover even when many Validators stop at once.
- **Slashing.** Applies to provable violations such as double signing. The Validator is forcibly exited and pays an immediate penalty plus a correlation penalty that grows with the amount of stake slashed around the same time. A coordinated attack is punished far more heavily than an isolated mistake.

> **The immediate penalty depends on the phase.** Before Phase 4 (Pectra) it is 1/32 of the effective balance (1 JOC); from Phase 4 it is 1/4096. **The immediate penalty is larger before Phase 4.**

## 4.7 Authority Layer

The Authority layer is the set of smart contracts on JOC that manages Validator entry and the flow of Validator funds. It does not depend on anything outside JOC or on other chains.

| Contract | Role |
| --- | --- |
| `ConsortiumManager` | Entry point of the Authority layer. Registers Validators, executes deposits, and performs forced exits. Only the Consortium Owner's Safe Multisig can operate it |
| `WithdrawReceiver` | One receiving contract per Validator. Receives rewards and exit proceeds and sends them only to the address the Validator declared |
| Deposit contract | Works the same as Ethereum's deposit contract. The only difference is that it accepts deposits only from `ConsortiumManager` |

### 4.7.1 Controlling Membership

On Ethereum, anyone who deposits 32 ETH can become a Validator. JOC's deposit contract accepts deposits only from `ConsortiumManager`, and `ConsortiumManager` executes only deposits whose destination is a `WithdrawReceiver` created by the consortium. This is the only change that separates PoSA from Ethereum PoS.

Like Ethereum's, the deposit contract itself cannot be upgraded, so this restriction is permanent.

### 4.7.2 Receiving Funds

Rewards and exit proceeds are sent from the consensus layer to each Validator's `WithdrawReceiver`. From there, the Validator withdraws them to the address it declared at registration. That address cannot be changed later, and the Consortium Owner cannot send the funds anywhere else (for the assumption about upgrade authority, see [4.4.2](#442-trust-assumptions)).

`WithdrawReceiver` contracts all point to one shared implementation (a Beacon Proxy). When a fix is needed, the `WithdrawReceiver` of every Validator can be updated in a single operation. This update authority also rests with the Consortium Owner's Safe Multisig.

### 4.7.3 How Exits Work

From Phase 4 (Pectra), EIP-7002 lets a smart contract request an exit. This adds two paths:

- The Validator requests its own exit from its `WithdrawReceiver`
- The Consortium Owner makes a Validator exit through `ConsortiumManager` (a forced exit)

A forced exit is the last resort for a Validator that does not respond or has lost its eligibility. Even in a forced exit, funds go only to the address the Validator declared. Slashing for double signing and similar violations is done automatically by the consensus layer and needs no action from the consortium.

The conventional exit signed with the Validator's key is available without waiting for Phase 4 ([4.8.3](#483-exit)).

## 4.8 Validator Lifecycle

### 4.8.1 From Joining to Operation

1. **Application and approval.** A company that wants to join applies to the Consortium Owner. Once approved, the Consortium Owner creates a `WithdrawReceiver` for that company and sends it the address.
2. **Key generation.** The Validator generates its keys in-house with the JOC version of the Deposit CLI. It sets the notified `WithdrawReceiver` as the destination and creates its deposit data (`deposit_data.json`).
3. **Deposit.** The Validator submits the deposit data to the JOC Launchpad. The Consortium Owner checks it and executes the 32 JOC deposit.
4. **Activation and operation.** Once the deposit is picked up by the beacon chain, the Validator becomes active. Allow roughly 3 hours from approval. From then on, the Validator Client performs attestations and block proposals automatically.

The beacon chain was set not to start until deposits for at least 8 Validators were in place. This condition was met on September 18, 2026, and the beacon chain has started.

### 4.8.2 Withdrawing Rewards

Rewards first accumulate in the Validator's balance on the beacon chain. From Phase 2 (Shapella), when withdrawals are enabled, any amount above 32 JOC is sent automatically to the `WithdrawReceiver`. The Validator then withdraws it to its declared address ([4.7.2](#472-receiving-funds)).

### 4.8.3 Exit

A Validator can exit on its own (a voluntary exit) in two ways, which become available at different times:

| Method | Available |
| --- | --- |
| Sign an exit message with the Validator's key and submit it (no contract call needed) | From 256 epochs (about 5.7 hours) after activation, including before Phase 1 (The Merge) |
| Request an exit from the `WithdrawReceiver` (requires the EIP-7002 fee) | From Phase 4 |

> **When you can exit and when you can recover your funds are different.** An exit signed with the Validator's key does not have to wait for Phase 1 (The Merge), but **even after exiting, funds cannot be withdrawn until Phase 2 (Shapella).** In an emergency such as a leaked key, a Validator can exit and leave the network without waiting for Phase 2.

After the exit, the remaining balance (32 JOC less penalties) is sent to the `WithdrawReceiver` in the same way as rewards. For forced exits by the Consortium Owner, see [4.7.3](#473-how-exits-work).
