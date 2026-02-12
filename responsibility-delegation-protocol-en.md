# Responsibility Delegation Protocol (RDP)

**Protocol Name:** Responsibility Delegation Protocol

**Version:** v0.1 (Concept Draft)

**Date:** 2026.03

**Editor:** HJS Sponsor

<p align="left">
  <a href="https://github.com/schchit/Responsibility-Delegation-Protocol
">
    <img src="https://img.shields.io/badge/Status-Public%20Proposal-blue" alt="Status">
  </a>
  <a href="https://creativecommons.org/licenses/by-sa/4.0/">
    <img src="https://img.shields.io/badge/License-CC_BY--SA_4.0-lightgrey" alt="License">
  </a>
  <a href="https://github.com/schchit/Responsibility-Delegation-Protocol/issues">
    <img src="https://img.shields.io/badge/Issues-Welcome-brightgreen" alt="Issues">
  </a>
  <a href="https://github.com/schchit/Responsibility-Delegation-Protocol/stargazers">
    <img src="https://img.shields.io/github/stars/schchit/Responsibility-Delegation-Protocol?style=social" alt="GitHub stars">
  </a>
</p>

---

## 0. Positioning

HJS inserts a judgment layer before decision execution, making human supervision recordable and verifiable.

Where does the right of judgment come from? Delegation.

The permission system answers "Who has the authority now".

The permission system does not answer: where the authority comes from, why it is granted, how long it is granted for, and whether it can be revoked.

**RDP is the protocol layer that records the fact of delegation.**

---

## 1. Problem

### 1.1 Definition

**Entrusted Evaporation**: The entrustment relationship is not recorded, or the record is unverifiable and untraceable, resulting in the breakage of the responsibility chain.

### 1.2 Three Types of Scenarios

**Oral Authorization**

The manager said in the instant message, "You'll handle the approvals for me this week."

The trustee executes the approval.

A misjudgment occurred three months later. The manager has since left the company.

System logs show that the approver is the trustee, and there is no record to prove that the approval authority comes from the delegation.

Audit Conclusion: The chain of responsibility broke at the first delegation.

**Subcontracting Black Hole**

Automobile manufacturers delegate road test analysis to outsourcing contractors.

Subcontractor's secondary subcontracting.

After the accident, the original principal claimed that "the task has been entrusted", the outsourcer claimed that "only management responsibility is assumed", and the subcontractor has been dissolved.

The principal-agent relationship never entered the auditable system. Responsibility completely evaporated within the subcontracting sequence.

**System Agent**

The monitoring system detected that the operator had exceeded the time limit and automatically transferred the decision-making authority to the backup duty officer.

Retrospective investigation after the incident revealed that the authority transfer rules were configured two years ago.

The rule configurator has transferred jobs.

The upstream approval record for approving this rule does not exist.

Humans transfer the delegation authority to the system, and the system does not record its own source of delegation.

### 1.3 Structural Defects

Common Structure of the Three Types of Scenarios:

- The delegation behavior occurs
- The entrustment behavior has not been formally recorded
- When making decisions, only the permission status is verified, and the permission source is not verified
- During the audit, the source of permissions cannot be traced

**In the current system architecture, delegation is the only form of responsibility transfer without an evidence layer.**

---

## 2. Definition

| Term | Definition |
|------|------------|
| **Responsibility Delegation** | A subject transfers its decision-making and judgment rights within a specific scope to another subject |
| **Client** | The entity initiating the delegation |
| **Trustee** | Entity accepting the commission |
| **Entrustment Certificate** | Data structure for recording delegation behavior, used for verification, revocation, and auditing |
| **Delegation Chain** | The sequence formed by valid delegation vouchers between the original responsible entity and the current executor |
| **Entrusted Evaporation** | The principal-agent relationship is not recorded or the record is unverifiable, resulting in the interruption of liability tracing |

The definition only describes structural characteristics and does not presuppose the legitimate source of the delegation.

---

## 3. Constraints

### 3.1 Structure cannot be bypassed

- The delegation action must be completed via the RDP protocol.
- Any decision-making authority must be traceable to the original responsible entity or valid delegation document
- The system shall not provide a permission configuration path that does not generate a delegation voucher
- Entrustment vouchers must be written into the non-tamperable storage layer

**This constraint is not configurable.**

If a bypass path exists, the credibility of all entrusted records will be reset to zero.

### 3.2 Two-way commitment

The entrustment must be signed and confirmed by the trustee.

- **Principal's Signature:** Granting Authority and Assuming Supervisory Responsibility
- **Trustee's signature:** Accept authority and assume responsibility for execution

Unconfirmed commission vouchers are invalid.

### 3.3 Explicit Range

The scope of delegation authority must clearly define its boundaries.

**Minimum Required Fields:**

- Decision Type
- Threshold Condition
- Validity Period

Full power of attorney must be explicitly declared and should have a clearly defined validity period.

### 3.4 Revocable

- The client may revoke the mandate at any time
- The revocation action generates a revocation voucher, which is associated with the original authorization voucher
- After the revocation takes effect, the permissions that depend on the delegation shall terminate within an acceptable time window
- The effectiveness of decisions made during the communication delay period shall be agreed upon in advance by the principal and the trustee

### 3.5 Auditable

- The delegation chain must be fully traceable
- The audit interface is open to compliance parties and regulatory parties
- Once the entrustment voucher is anchored, it cannot be deleted

---

## 4. Data Structure

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

**Undetermined:**

- Identity Identification Format (DID/email/AD)
- Complexity of range expressions (AND/OR/nesting)
- The entity that generates vouchers for system-automated delegation

---

## 5. Location

**RDP is the pre-protocol of HJS.**

```
Delegation Credential → HJS Judgment Record
```

- **HJS:** Record "Who made the judgment"
- **RDP:** Record "who has the authority to make this judgment and where the authority comes from"

RDP does not depend on HJS. It can be independently deployed in any system that needs to record the principal-agent relationship.

---

## 6. Open Questions

### 6.1 Entrustment Depth

Should the delegation chain have a length limit? If so, how many levels?

### 6.2 Cross-Domain Delegation

When Organization A authorizes personnel from Organization B, how is the authorization certificate verified? Is a global trust anchor required?

### 6.3 Undo Delay

After the cancellation of voucher generation, within how long should the nodes of cached vouchers become invalid? Are the decisions made during the delay period valid?

### 6.4 Emergency Entrustment

Is it allowed to submit the entrusted vouchers after the fact? What is the time limit for reissuing them? Can the reissued vouchers cover the decisions made during the emergency period?

### 6.5 System Delegation

Can humans pre-authorize delegation strategies? In what data structure should the strategy itself be stored as evidence?

### 6.6 Identity Compatibility

Should a specific identity format be mandatory? How can cross-system delegation credentials be ensured to be mutually recognized?

### 6.7 Role Identification

role field values lack a unified vocabulary. During cross-organizational audits, how can we map role permissions from different naming systems? Is a public role registry needed?

---

## 7. Open Source

**License Text:** CC BY-SA 4.0

**Example code:** To be contributed

---

## 8. Participation

**Contribution Method:**

- **Issue:** Point out errors, omissions, or better designs
- **Pull Request:** Modify text, supplement use cases, and provide sample code

---

## 9. Protocol Family

RDP is the first extension protocol of the HJS Protocol Family.

**Planned extensions:**

- **Responsibility Termination Statement (RTS)** — Formalizing when and how responsibility ends, preventing infinite liability.
- **Responsibility Conflict Resolution Framework (RCRF)** — Computable attribution of responsibility when multiple parties are involved.

These are **not active drafts**. They are identified gaps. We welcome discussion before formalization.

**Special Needs:**

- Architects with experience in enterprise commissioned approval practices
- Legal practitioners familiar with the Electronic Signature Law and Evidence Rules
- Practitioners who have dealt with cross-domain delegation compliance issues

---

**GitHub / Issues / CC BY-SA 4.0**

*Making automated systems more accountable, making human judgment more valuable.*
