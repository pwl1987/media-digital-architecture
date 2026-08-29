# Portfolio Recovery Program V1

## Goal

将现有仓库从“项目集合”转化为可治理的产品/能力组合。默认动作不是继续补旧功能，而是先判断价值、完成度和架构位置。

## Workstreams

### W0 — Freeze the portfolio

新功能不得在重复/待判定项目中继续扩张。只有安全修复、数据保存和必要运维修复允许进入冻结项目。

### W1 — Evidence audit

每个项目必须建立：

- claimed capabilities
- implemented capabilities
- integrated paths
- verified runtime evidence
- production evidence
- missing/placeholder paths

### W2 — Canonical model

先统一 `Asset / Artifact / Task / Job / Generation / Knowledge / Dataset / Model / Evidence`，再迁移代码。

### W3 — Core platform selection

当前默认主骨架：

- `news-media-system` → Business / Content Control Plane
- `YimengSpirit-Multimodal` → Intelligence Plane
- `VBMF` → Broadcast Runtime
- `live-platform` → Live Operations
- Creative domain → consolidation of `media-ai-platform` + `lamice` + `lamice-platform`

### W4 — Extract engines

将专项算法/处理能力变成契约化引擎：

- shot detection
- compression / quality gate
- ASR / OCR / media normalization as appropriate

### W5 — Experience platform

建立 `media-digital-platform` 作为统一入口/体验壳：SSO、导航、workspace、搜索、任务中心、通知、module registry、Design System。

### W6 — Legacy retirement

当替代能力通过生产证据验证后，关闭旧项目新功能入口，进入只读/归档/退休。

## Recovery decision tree

```text
Is there real business/user value?
 ├─ No → Freeze / Retire
 └─ Yes
     │
     ├─ Is the existing implementation healthy and aligned?
     │    ├─ Yes → Recover
     │    └─ No
     │        │
     │        ├─ Valuable algorithms/data/UX?
     │        │    ├─ Yes → Extract + Rebuild
     │        │    └─ No → Rebuild from canonical model
```

## Completion gate

A capability is `Complete` only when the user-visible path, API/command, persistence/state, runtime execution, result/artifact, failure/recovery and automated verification are all evidenced. A test count alone cannot satisfy the gate.

## Do-not-repeat rules

- Do not create another CMS because the existing CMS feels uncomfortable; fix/rebuild the owned domain or create a deliberate replacement ADR.
- Do not create another AI gateway because a provider integration is inconvenient.
- Do not create a new media asset model in a creative application.
- Do not make URL strings the canonical identity of generated media.
- Do not fork a product into a new stack without an explicit migration rationale.
- Do not let research code become a production dependency by convenience.
- Do not interpret documentation “✅” as runtime proof.

## Exit criteria for portfolio recovery

Portfolio recovery is complete only when:

1. every in-scope repository has a declared owner/domain/role/lifecycle;
2. every duplicate capability has one canonical owner;
3. cross-system contracts have versioned definitions;
4. critical migrations have rollback and verification procedures;
5. legacy repositories are frozen or retired where appropriate;
6. the theme platform can expose the ecosystem without copying domain data or logic.
