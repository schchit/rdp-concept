# Responsibility Delegation Protocol (RDP)

<p align="center">
  <a href="README.zh-CN.md">中文</a> | <strong>English</strong>
</p>

<p align="center">
 
  <a href="https://creativecommons.org/licenses/by-sa/4.0/">
    <img src="https://img.shields.io/badge/License-CC_BY--SA_4.0-lightgrey" alt="License">
  </a>
 
</p>

The **Responsibility Delegation Protocol (RDP)** is the protocol layer that records the fact of delegation. It is the pre-protocol of [HJS (Human Judgment System)](../README.md).

---

## What This Directory Contains

### Positioning

- **HJS** inserts a judgment layer before decision execution and records "who made the judgment."
- **RDP** records "who has the authority to make this judgment and where that authority comes from"—i.e., the source and chain of delegation.
- Permission systems answer "who has authority now" but not where it came from, why it was granted, for how long, or whether it can be revoked. **RDP fills the evidence-layer gap for delegation as a form of responsibility transfer.**

### Core Problem

**Entrusted Evaporation**: The delegation relationship is not recorded, or the record is unverifiable and untraceable, leading to a broken chain of responsibility.

The documents illustrate this with three typical scenarios: oral authorization, subcontracting black hole, and system agent. In all three, delegation is not formally recorded, only permission status is checked at decision time (not permission source), and the source cannot be traced in audits.

### Key Concepts

| Concept | Description |
|---------|-------------|
| Responsibility Delegation | A subject transfers its decision-making and judgment rights within a specific scope to another subject |
| Client | The entity initiating the delegation |
| Trustee | The entity accepting the delegation |
| Entrustment Certificate | Data structure that records delegation behavior, used for verification, revocation, and auditing |
| Delegation Chain | The sequence of valid delegation vouchers from the original responsible entity to the current executor |

### Protocol Constraints (Summary)

- **Structure cannot be bypassed**: Delegation must be completed via the RDP protocol; vouchers must be written to non-tamperable storage; no permission configuration path may exist that does not generate a delegation voucher.
- **Two-way commitment**: Delegation must be signed and confirmed by both principal and trustee; unconfirmed vouchers are invalid.
- **Explicit scope**: Delegation authority must define boundaries (decision type, threshold conditions, validity period, etc.).
- **Revocable and auditable**: The principal may revoke at any time; the delegation chain must be fully traceable; the audit interface is open to compliance and regulatory parties.

### Relation to HJS

```
Delegation Credential (RDP) → HJS Judgment Record
```

RDP does not depend on HJS and can be deployed independently in any system that needs to record delegation relationships.

---

## Document Index

- **English (full text):** [responsibility-delegation-protocol-en.md](responsibility-delegation-protocol-en.md)
- **中文（全文）:** [responsibility-delegation-protocol-zh-CN.md](responsibility-delegation-protocol-zh-CN.md)

**Version:** v0.1 (Concept Draft) · **License:** CC BY-SA 4.0
