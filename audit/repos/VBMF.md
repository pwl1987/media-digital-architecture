# Archaeology — VBMF

## 定位

VBMF 不是烂尾业务项目，而是**规范成熟、实现仍在建设中的专业 Realtime Broadcast Fabric**。

README 明确 V0.2 Runtime Semantics CLOSED，架构基线经过 22 轮 review；Phase 0.5 的 operator/UI semantics 也已锁定，但 Reference Implementation 进入 Phase 0.6，Media Agent/完整 Web Console 仍在后续阶段。fileciteturn177file0L2-L2

## 关键判断

### 1. 最大风险不是“代码不够”，而是规范先跑得远

架构、对象、surface、故障语义已大量锁定；实现还在追赶。后续必须建立“implemented/verified”证据，不得继续扩张规范规模而不完成执行链。

### 2. 不能被普通 Web 平台吞掉

Source / Signal Fabric / Normalize / Redundancy / QC / Playout / Switcher / Composition / Audio / Output / Recording / Replay 以及 Health Tree、Watchdog、Capability Registry 等构成广播专业域。fileciteturn177file0L2-L2

### 3. UI 设计资产很有价值

Phase 0.5 已形成较完整的 operator surface、navigation、design system、i18n 和操作链语义；这些可以作为专业运维 UI 的高质量资产，但不等于必须把 VBMF UI 技术栈统一成企业业务 UI。

## 资产价值

极高：

- Runtime semantics
- Health Tree
- Switch modes / hot standby model
- Capability Registry
- Configuration Versioning
- Incident Timeline
- Operator workflow
- Fault injection acceptance model

## 不应迁移

- 不能把 VBMF DB/model 直接并入 news-media business schema。
- 不能把 BroadcastSession 等实时对象当成普通 CRUD Job。
- 不能让 Web UI 依赖 DeckLink/GStreamer 内部实现。

## 最终命运

**Protect + Implement**

保护其架构边界；下一阶段重点不是再设计，而是执行 Phase 0.6/1 的可执行验收，逐步把锁定语义转化为真实 runtime。

## 母架构接入

上层只调用：

```text
Broadcast Control API
Session / Source / Health / Switch / Recording
```

底层保持 Rust/GStreamer/FFmpeg/DeckLink 等独立。
