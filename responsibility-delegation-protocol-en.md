# Responsibility Delegation Protocol (RDP)

<p align="center">
  <a href="CN-responsibility-delegation-protocol.md">中文</a> | <strong>English</strong>
</p>

**Protocol Name:** Responsibility Delegation Protocol
**Version:** v0.1 (Concept Draft)
**Date:** February 2026
**Editor:** HJS Editor

<p align="left">
  <a href="https://github.com/schchit/Responsibility-Delegation-Protocol">
    <img src="https://img.shields.io/badge/Status-Draft-blue" alt="Status">
  </a>
  <a href="https://creativecommons.org/licenses/by-sa/4.0/">
    <img src="https://img.shields.io/badge/License-CC_BY--SA_4.0-lightgrey" alt="License">
  </a>
  <a href="https://github.com/schchit/Responsibility-Delegation-Protocol/issues">
    <img src="https://img.shields.io/badge/Issues-Welcome-brightgreen" alt="Issues">
  </a>
</p>

---

## 0. Positioning

HJS records verifiable human judgment before irreversible decisions. RDP records the source of that judgment authority — delegation.

Permission systems answer "who currently has access." They do not answer where that authority came from, why it was granted, how long it lasts, or whether it can be revoked. RDP provides a protocol layer for recording delegation facts.

---

## 1. Problem

### 1.1 Definition

**Delegation Evaporation**: Delegation relationships are unrecorded or non‑verifiable, leading to broken accountability chains.

### 1.2 Three Common Scenarios

**Verbal Authorization**
A manager says in an instant message: "You'll handle approvals for me this week." The delegatee executes approvals. Three months later, a misjudgment occurs. The manager has left. System logs show the delegatee as the approver, but no record proves the approval authority came from the manager. Audit conclusion: the accountability chain breaks at the first delegation.

**Subcontracting Chain**
An automaker delegates road‑test analysis to an outsourcer. The outsourcer sub‑delegates to freelancers. After an incident, the principal claims "the task was delegated," the outsourcer claims "we only managed," and the subcontractor has dissolved. Delegation relationships never entered any auditable system. Accountability evaporates completely in the subcontracting chain.

**System‑Automated Delegation**
A monitoring system detects operator timeout and automatically transfers decision authority to a backup operator. After an incident, investigation reveals the transfer rule was configured two years ago. The rule configurer has changed roles. No upstream approval record for the rule exists. Authority transfers occur without traceable delegation records.

### 1.3 Structural Gap

All three scenarios share the same structure:

1. Delegation occurs.
2. Delegation is not formally recorded.
3. Decision execution checks only the permission state, not the permission source.
4. Audits cannot trace the permission source.

In current system architectures, delegation is the only form of responsibility transfer without an evidence layer.

---

## 2. Core Concepts

| Term | Description |
|------|-------------|
| **Delegation** | Transfer of decision authority within a specific scope from one entity to another |
| **Delegator** | Entity initiating the delegation |
| **Delegatee** | Entity receiving the delegation |
| **Delegation Credential** | Data structure recording the delegation act |
| **Delegation Chain** | Sequence of credentials from original authority to current executor |
| **Delegation Evaporation** | Delegation relationships unrecorded or non‑verifiable, breaking accountability chains |

Definitions describe structural characteristics only; they do not presuppose legal validity.

---

## 3. Protocol Constraints

### 3.1 Non‑circumventable Structure
- Delegation must use RDP
- Every decision authority must be traceable to an original responsible entity or a valid delegation credential
- Systems must not provide permission‑configuration paths that bypass credential generation
- Delegation credentials must be written to an immutable storage layer

*This constraint is not configurable.*

### 3.2 Two‑Party Consent
- Delegation requires signatures from both delegator and delegatee
- Delegator signature grants authority
- Delegatee signature accepts authority
- Unsigned credentials are invalid

### 3.3 Explicit Scope
- Decision types
- Threshold conditions
- Validity period

*Full delegation must be explicitly declared and have a clear validity period.*

### 3.4 Revocable
- Delegators may revoke at any time
- Revocation generates a record linked to the original credential
- After revocation, permissions terminate within an acceptable time window
- Decision validity during propagation delay should be agreed in advance

### 3.5 Auditable
- Delegation chains must be fully traceable
- Audit interfaces open to compliance and regulatory bodies
- Credentials cannot be deleted once anchored

---

## 4. Data Structure (Speculative)

```json
{
  "protocol": "RDP/1.0",
  "credential_id": "rdp-20260312-001",
  "delegator": {
    "id": "alice@bank.com",
    "role": "senior_risk_officer"
  },
  "delegatee": {
    "id": "bob@bank.com",
    "role": "interim_risk_officer"
  },
  "scope": {
    "decision_types": ["account_freeze"],
    "threshold": {
      "amount": 100000,
      "currency": "USD"
    }
  },
  "validity": {
    "from": "2026-03-12T00:00:00Z",
    "until": "2026-06-11T23:59:59Z",
    "revocable": true
  },
  "delegation_proof": {
    "delegator_signature": "0x7a8b...",
    "delegatee_signature": "0x3c4d...",
    "timestamp": "2026-03-12T09:30:15Z"
  }
}
```
Undetermined:

Identity format (DID/email/AD)

Scope expression complexity (AND/OR/nesting)

Credential issuer for system‑automated delegation

5. Position Relative to HJS
text
Delegation Credential (RDP) → HJS Judgment Record
HJS: records who executed a judgment

RDP: records who had authority to execute that judgment and where that authority came from

RDP does not depend on HJS and can be deployed independently in any system that needs to record delegation relationships.

6. Open Issues
6.1 Delegation Depth — Should delegation chains have a maximum length? If so, how many levels?

6.2 Cross‑Domain Delegation — When Organization A authorizes someone in Organization B, how are credentials verified? Is a global trust anchor needed?

6.3 Revocation Latency — After a revocation credential is generated, how long should cached credentials remain active? Are decisions made during the latency window valid?

6.4 Emergency Delegation — Should post‑event delegation credentials be allowed? What is an acceptable grace period? Can a post‑event credential retroactively cover decisions made during the emergency?

6.5 System‑Automated Delegation — Can humans pre‑authorize delegation policies? How should such policies themselves be recorded?

6.6 Identity Compatibility — Should RDP mandate a specific identity format? How can cross‑system interoperability be ensured if legacy identities (email, AD) are supported?

6.7 Role Semantics — The role field lacks a controlled vocabulary. How can different naming systems be mapped during cross‑organizational audits? Is a public role registry needed?

7. Open Source
License: CC BY-SA 4.0

Sample Code: To be contributed

Anyone may implement commercial or non‑commercial products based on this draft. No license fees are required.

8. Participation
Ways to contribute:

Issue: Point out errors, omissions, or better designs

Pull Request: Revise text, add use cases, or provide sample code

Especially needed:

Architects with experience in enterprise delegation/approval workflows

Legal professionals familiar with electronic signature laws and rules of evidence

Practitioners who have handled cross‑domain delegation compliance

9. Protocol Family
RDP is the first extension protocol of the HJS Protocol Family.

Planned extensions:

Responsibility Termination Statement (RTS) — Records when and how responsibility ends

Responsibility Conflict Resolution Framework (RCRF) — Provides structured evidence for responsibility attribution when multiple parties are involved

These are not active drafts. They are identified gaps. We welcome discussion before formalization.

GitHub / Issues / CC BY-SA 4.0

RDP v0.1


