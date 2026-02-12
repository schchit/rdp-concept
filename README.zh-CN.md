# Responsibility Delegation Protocol (RDP)

<p align="center">
  <strong>中文</strong> | <a href="README.md">English</a>
</p>

**责任委托协议（RDP）** 是记录委托事实的协议层，为 [HJS（人类判断系统）](../README.zh-CN.md) 的前置协议。

---

## 本目录文档主要内容

### 定位

- **HJS** 在决策执行前插入判断层，记录“谁执行了判断”。
- **RDP** 记录“谁有权执行此判断、权从何来”——即委托关系的来源与链条。
- 权限系统只回答“现在谁有权”，不回答权从何来、为何授予、授予多久、能否撤回。**RDP 填补委托这一责任转移形式的证据层缺失。**

### 核心问题

**委托蒸发（Entrusted Evaporation）**：委托关系未被记录，或记录不可验证、不可追溯，导致责任链断裂。

文档通过三类典型场景说明问题：口头授权、转包黑洞、系统代理——共同点都是委托行为未形式化记录，决策时只校验权限状态不校验权限来源，审计时无法追溯。

### 核心概念

| 概念 | 说明 |
|------|------|
| 责任委托 | 主体将特定范围内的决策判断权转移给另一主体 |
| 委托人 | 发起委托的主体 |
| 受托人 | 接受委托的主体 |
| 委托凭证 | 记录委托行为的数据结构，用于验证、撤销、审计 |
| 委托链 | 从原始责任主体到当前执行者之间，有效委托凭证构成的序列 |

### 协议约束要点

- **结构不可绕过**：委托须经 RDP 协议完成，凭证须写入不可篡改存储，不得提供不生成凭证的权限配置路径。
- **双向承诺**：委托须委托人、受托人双方签名确认，未确认的委托凭证无效。
- **显式范围**：委托权限须明确决策类型、阈值条件、有效期等边界。
- **可撤销、可审计**：委托人可随时撤销；委托链须完整可追溯，审计接口向合规方、监管方开放。

### 与 HJS 的关系

```
委托凭证 (RDP) → HJS 判断记录
```

RDP 不依赖 HJS，可独立部署于任何需要记录委托关系的系统。

---

## 文档索引

- **English (full text):** [responsibility-delegation-protocol-en.md](responsibility-delegation-protocol-en.md)
- **中文（全文）:** [responsibility-delegation-protocol-zh-CN.md](responsibility-delegation-protocol-zh-CN.md)

**Version:** v0.1 (Concept Draft) · **License:** CC BY-SA 4.0
