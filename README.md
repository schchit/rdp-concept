# Responsibility Delegation Protocol (RDP)
<p align="center">
  <a href="README.zh-CN.md">中文</a> | <strong>English</strong>
</p>

<p align="center">
  <a href="#"><img src="https://img.shields.io/badge/Status-Draft-blue" alt="Status"></a>
  <a href="https://creativecommons.org/licenses/by-sa/4.0/"><img src="https://img.shields.io/badge/License-CC_BY--SA_4.0-lightgrey" alt="License"></a>
  <a href="#"><img src="https://img.shields.io/badge/Issues-Welcome-brightgreen" alt="Issues"></a>
  <a href="#"><img src="https://img.shields.io/github/stars/hjs-spec/spec?style=social" alt="GitHub stars"></a>
</p>

Responsibility Delegation Protocol (RDP) is a protocol layer for recording delegation facts, used alongside the HJS core protocol.

## Overview

HJS records who executed a judgment. RDP records who had the authority to execute that judgment and where that authority came from.

Permission systems answer "who currently has access." They do not answer where that authority came from, why it was granted, how long it lasts, or whether it can be revoked. RDP fills this gap by providing an evidence layer for delegation.

## Core Problem

**Delegation Evaporation**: Delegation relationships are unrecorded or non‑verifiable, leading to broken accountability chains.

Three common scenarios illustrate the problem:
- Verbal authorization via informal channels
- Subcontracting chains where authority becomes untraceable
- System‑automated delegation with no record of the authorizing rule

In each case, delegation occurs without formal recording, decisions check only current permissions, and audits cannot trace authority sources.

## Core Concepts

| Term | Description |
|------|-------------|
| Delegation | Transfer of decision authority within a specific scope |
| Delegator | Entity initiating the delegation |
| Delegatee | Entity receiving the delegation |
| Delegation Credential | Data structure recording the delegation act |
| Delegation Chain | Sequence of credentials from original authority to current executor |

## Protocol Constraints

- **Non‑circumventable**: Delegation must use RDP
- **Immutable storage**: Credentials written to immutable storage
- **No bypass**: No permission paths that bypass credential generation
- **Two‑party consent**: Delegation requires signatures from both delegator and delegatee
- **Explicit scope**: Decision types, thresholds, validity periods must be clearly defined
- **Revocable**: Delegators can revoke at any time
- **Auditable**: Chains must be fully traceable

## Relationship with HJS
Delegation Credential (RDP) → HJS Judgment Record

text

RDP can be deployed independently in any system that needs to record delegation relationships.

## Documents
## 📄 Full Specification

View the complete protocol specification:
- [English Full Version](spec/responsibility-delegation-protocol.md)
- [Chinese Full Version](spec/责任委托协议.md)

**Version:** v0.1 (Concept Draft) · **License:** CC BY-SA 4.0
