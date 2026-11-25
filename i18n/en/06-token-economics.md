---
title: 6. Token Economics
navigation:
  order: 160
---

# 6. Token Economics

JOC's economic design is calibrated for a consortium-scale Validator set rather than for permissionless participation.

## 6.1 The Role and Benefits of the JOC Crypto-Asset

The JOC crypto-asset, at the center of Japan Open Chain, is the fee currency required for the many kinds of transactions on the platform: transfers, NFT minting, smart-contract deployment, and more. In other words, anyone transacting on Japan Open Chain must pay the fee in JOC. The fee can also be paid by someone else, so in some cases the parties to a transaction need not bear it.

Under PoSA, the JOC crypto-asset has three uses:

| Use | Description |
| --- | --- |
| Paying fees | Paid as gas for every transaction: transfers, smart-contract execution, NFT minting, and so on (a third party can also bear the fee) |
| Validator rewards | The Validator that proposes a block receives the transaction fees (priority fees). Consensus-layer issuance ([6.5](#65-consensus-layer-issuance)) is added to rewards |
| Validator stake | 32 JOC per Validator, subject to slashing |

Validators verify the authenticity of transactions and propose and attest to new blocks. Receiving JOC in return forms the foundation of this ecosystem.

As on Ethereum, the JOC fee mechanism adjusts dynamically with market supply and demand, keeping it fair and transparent. When demand for Japan Open Chain grows, the price of JOC rises, and when demand overheats, the rising price helps restrain traffic. This balance of supply and demand keeps Japan Open Chain's traffic stable.

The JOC crypto-asset is also used to fund grants and financing for contributors and external developers who are expected to help the Japan Open Chain ecosystem grow, encouraging the development of new applications and DApps. Developers who receive JOC can expect its value to rise, like shares or stock options, if their work expands the ecosystem.

## 6.2 Total Supply

The initial total supply of the JOC crypto-asset was **1 billion JOC**, all minted at network creation (genesis). The former PoA (Clique) had no block reward, so supply did not increase during the PoA period.

With the move to PoSA in the Tokyo Hard Fork, new JOC is created automatically as Validator rewards under the consensus-layer protocol. The former fixed supply cap is therefore removed, and total supply changes with protocol issuance, burns, and similar factors.

This issuance follows a predefined protocol; Japan Blockchain Foundation Inc. does not issue additional JOC at its discretion.

From PoSA onward, total supply is:

```
supply(t) = 1,000,000,000 JOC − cumulative burn(t) + cumulative issuance(t)
```

- **Burn.** The EIP-1559 base fee is burned ([6.3](#63-transaction-fee-mechanism)).
- **Issuance.** The rewards the consensus layer pays to Validators ([6.5](#65-consensus-layer-issuance)).
- **Deposits do not change total supply.** A 32 JOC deposit moves into the Deposit Contract, reducing circulating supply, but total supply is unchanged.

> **On the scale of the burn.** JOC blocks come every 5 seconds, and block usage is far below the gas target, so the base fee sits near its floor (measured in August 2026). The amount burned is negligible compared with issuance, so **after PoSA, JOC's total supply grows slowly by essentially the amount issued.** That growth is very small relative to supply: about 0.0009% of supply per year with about 25 Validators ([6.5](#65-consensus-layer-issuance)).

## 6.3 Transaction Fee Mechanism

JOC fees work as they do on Ethereum (EIP-1559).

### 6.3.1 Gas

Gas pays for transactions on the Japan Open Chain blockchain. The amount needed depends on how complex the transaction is. A simple JOC transfer needs 21,000 gas; more complex transactions (for example, those used in DeFi) can need more than 1,000,000 gas.

### 6.3.2 Gas Price

Gas has a price, called the "gas price". It is quoted in gwei, where 1 JOC = 1 × 10^9 (1,000,000,000) gwei. At a gas price of 100 gwei, a 21,000-gas transaction costs 21,000 × 100 = 2,100,000 gwei (0.0021 JOC).

The amount of gas a transaction needs is fixed, but the gas price varies. The user sets the gas price when sending a transaction (often done automatically by wallet software). The gas price has two parts:

- **Base fee — burned.** It adjusts automatically with block usage and is burned.
- **Priority fee — to the block proposer.** The priority fee a user adds goes directly to the `fee_recipient` address specified by the Validator that proposed the block. It is a transfer to the Validator and does not change total supply.

## 6.4 Relationship with Stablecoins

Stablecoins are planned to be issued on Japan Open Chain under the ERC-20 standard. The JOC crypto-asset is used as the fee currency for stablecoin transfers, so every time a stablecoin is issued and transferred on Japan Open Chain, JOC is consumed.

Since stablecoins are expected to be at the center of all web3 financial transactions, how much stablecoin is issued on a blockchain affects the price of that blockchain's fee currency, JOC.

As various banks issue stablecoins on Japan Open Chain, the value of Japan Open Chain's token is expected to rise, benefiting everyone in the Japan Open Chain community.

## 6.5 Consensus-Layer Issuance

The consensus layer pays Validators with the same formula as Ethereum. The base reward per Validator per epoch is:

```
base reward = effective balance × BASE_REWARD_FACTOR ÷ √(total active stake)
```

JOC uses the Gnosis preset, so `BASE_REWARD_FACTOR` is **25** (64 on Ethereum mainnet). It is a preset constant and cannot be changed in `config.yaml`. The formula has these consequences:

- **Issuance scales with the square root of total stake.** Annual issuance is roughly `311.64 × √(total active stake [JOC])`. Doubling the number of Validators raises total issuance by only about 41% and lowers each Validator's reward by about 29%.
- **Issuance is very small relative to supply.** With a Validator set of about 25, annual issuance is roughly 8,800 JOC (about 0.0009% of supply). Even if 100% of supply were staked, annual issuance could not exceed about 0.99%.
- **There is no compounding.** With `0x01` withdrawal credentials the effective balance is capped at 32 JOC, so any balance above it is swept to the `WithdrawReceiver` (from Phase 2). Total active stake stays at `32 JOC × number of Validators`, and issuance is linear.
- **It scales with participation.** Missed attestations and offline periods reduce rewards or incur penalties ([4.6.3](04-japan-open-chain.md#463-validator-duties-rewards-and-penalties)).

## 6.6 Validator Income

A Validator's income has two streams:

| Income | Source | Where it arrives | What drives it |
| --- | --- | --- | --- |
| Consensus rewards (issuance) | The consensus layer ([6.5](#65-consensus-layer-issuance)) | The Validator balance on the Beacon Chain; the part above 32 JOC goes to the `WithdrawReceiver` from Phase 2 | Number of Validators (diluted as 1/√N), participation |
| Priority fee | The user who sent the transaction | The `fee_recipient` specified by the Validator that proposed the block | Transaction volume and fee level (diluted as 1/N with N Validators) |

The ratio between the two streams depends on the number of Validators and on transaction volume. Because priority fees depend on transaction volume, they become a larger share as network usage grows. Either way, income can ultimately only be withdrawn to the address the Validator declared in advance ([4.8.2](04-japan-open-chain.md#482-withdrawing-rewards)).

## 6.7 Network Parameters and Dual-Track Security

| Parameter | Value | Rationale |
| --- | --- | --- |
| Stake per Validator | 32 JOC | Matches Ethereum; familiar tooling, well-understood security properties |
| Minimum genesis Validators | 8 | Below this, the chain does not start |
| Slot | 5 seconds | Preserves the PoA-era block time |
| Epoch | 16 slots (80 seconds) | Gnosis preset; consistent with a 5-second slot |
| Finality | ~2 epochs (about 2.7 minutes) | Faster than Ethereum mainnet's ~13 minutes (as of November 2026), because slots and epochs are shorter |
| `BASE_REWARD_FACTOR` | 25 | Gnosis preset (64 on Ethereum mainnet) |

The 32 JOC stake was chosen less for its size as capital than so that JOC can use the same tools and security model as Ethereum. JOC's security does not come from the size of individual stakes; it comes from the combination of:

1. **On-chain slashing.** Each Validator's stake is confiscated for provable misbehavior.
2. **Off-chain contracts.** Contracts among the Validators are binding under Japanese contract law.

The stake per Validator is small, while the legal responsibility each Validator carries is large — two mechanisms working together. This is where JOC differs from Ethereum mainnet, which relies on stake alone for security. And because the consortium approves Validator entry ([4.7.1](04-japan-open-chain.md#471-controlling-membership)), no one can take over the network simply by staking more.

Inactivity-leak and similar parameters are defined by the preset (gnosis) constants and the `config.yaml` distributed by the consortium ahead of each fork. For the confirmed values, see `config.yaml` ([Reference 9](12-references.md#references)).
