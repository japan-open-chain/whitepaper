---
title: 10. Project Risks
navigation:
  order: 200
---

# 10. Project Risks

## 10.1 Community Risk

The success of the project depends heavily on an active and healthy community. If the community becomes inactive or internal conflict arises, development and progress may be delayed. Losing the community's trust could also lower the project's reputation and value.

## 10.2 Security Risks and Countermeasures

Japan Open Chain achieves high security through a defense-in-depth model, and continuously addresses the following potential risks.

### 10.2.1 Responding to Advances in Cryptography

**Risk:** the arrival of quantum computers and rapid advances in cryptography

**Countermeasures:**

- R&D on quantum-resistant cryptography (full-scale introduction planned for the v4 Kyoto Hard Fork)
- Keeping up with the latest security standards
- Regular security audits and updates

### 10.2.2 Validator Security

**Risk:** simultaneous compromise of a majority of Validators

**Countermeasures:**

- Risk distribution through the three-tier Validator structure (planned for the Osaka Hard Fork)
- Economic security through staking and slashing ([4.6.3](04-japan-open-chain.md#463-validator-duties-rewards-and-penalties))
- Strict screening and KYC of Core Validators
- Anomaly detection through on-chain monitoring

### 10.2.3 Continuous Security Improvement

Japan Open Chain continuously strengthens its security through the following measures:

- **Regular audits:** quarterly security audits and penetration tests
- **Bug bounty:** a vulnerability disclosure program
- **Incident response:** 24/7 monitoring and response team
- **Community collaboration:** transparent sharing of security information
- **Technical updates:** prompt application of the latest Ethereum security patches

## 10.3 Residual Design Risks

The PoSA design does not remove the following risks.

- **Collusion between the consortium and a Validator majority** ([4.4.2](04-japan-open-chain.md#442-trust-assumptions)). Deterrence relies on legal agreements among the participants.
- **Contract upgrade authority.** The Authority layer contracts are upgradeable, and that authority rests with the Consortium Owner's Safe Multisig ([4.4.2](04-japan-open-chain.md#442-trust-assumptions)). Abuse of the authority or compromise of the multisig keys could affect the flow of Validator funds.
- **Regulatory change.** Changes to laws and regulations on crypto-assets or staking could affect how the network is operated and how the token is handled.
- **Migration risk.** Each phase of the Tokyo Hard Fork requires client updates and network-wide coordination. If a defect is found, a phase may be postponed or its configuration corrected.
- **Operational mistakes by Validators.** Key management, missed client updates, and penalties from being offline are the operator's responsibility.
- **Client bugs.** Multiple execution-client implementations reduce this risk but do not eliminate it.
- **Token price and fee-level fluctuation.** Validator income varies with the JOC price and transaction volume. This paper does not guarantee income.
- **Changes to plans.** The timing of each phase and parameter values may be changed at the consortium's discretion.
