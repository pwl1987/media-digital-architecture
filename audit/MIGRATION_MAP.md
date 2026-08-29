# Migration Map — Draft 0.1

## 1. General rule

不要“大合库”。迁移的是**能力、数据、契约和设计资产**，不是把所有源码揉成一个仓库。

## 2. `media-platform` → `news-media-system`

### Migrate

- 领域设计中仍有价值的 Content/Media 语义
- Storage abstraction 思路
- 安全策略与审计经验
- 有价值的 migration/test assets
- 可验证的业务规则

### Freeze

- 新功能开发
- 第二套融媒体主 API
- 第二套用户/权限事实源
- 第二套媒体资产事实源

### Retire after migration

旧业务 CRUD 与重复基础设施。

## 3. `media-ai-platform` + `LAMICE`

目标不是简单 merge repository，而是明确：

```text
AI Video Production Platform
        ↑
LAMICE Creative Studio
```

### Platform owns

- CreativeProject
- Generation
- AI capability orchestration
- Job lifecycle
- Artifact lifecycle
- Provider/model abstraction
- Timeline/render orchestration
- Usage/audit where required

### Studio owns

- UX
- Editor interaction
- Storyboard workspace
- Timeline interaction
- Creative review
- Human-in-the-loop workflows

### Must eliminate

- duplicate Project model
- duplicate media URL truth
- duplicate Provider registry
- duplicate task orchestration semantics
- duplicate asset lifecycle

## 4. `video-shot-detection`

保持独立 Engine，补齐标准输入输出 Contract：

```text
input Artifact → Job → VideoShot artifacts + metadata → Event
```

## 5. `video-compression-system`

保持独立 Engine，标准化：

```text
source Artifact
 → encode profile
 → quality evaluation
 → derived Artifact
 → quality report
```

## 6. `live-platform` + `VBMF`

不合库。

建立：

```text
Business/Operations
       ↓
Live/Broadcast Control API
       ↓
Runtime
```

`live-platform` 管 streaming operations；`VBMF` 管 broadcast-grade realtime media runtime。

## 7. `yimengjingshen`

保留为 Research Lab。

输出必须进入：

```text
Dataset Artifact
Model Artifact
Evaluation Artifact
Experiment Record
```

生产系统只消费注册后的 Model Artifact，不依赖研究仓库源码。

## 8. `YimengSpirit-Multimodal`

逐步成为领域 Intelligence Plane：

- Knowledge
- Evidence
- Multimodal retrieval
- Model serving abstraction
- AI capability
- Evaluation

它不应该成为新闻 CMS，也不应该成为 Creative Studio。

## 9. `ai-spider-annotation`

演进为 Data Studio：

```text
Collect → Clean → Annotate → Review → Dataset → Export
```

Dataset 必须可追溯到来源 Artifact / Evidence。

## 10. `xiao-opera-miniapp`

保持 Consumer Application 定位。

只通过正式 API 获取内容、知识和生成能力，不直接访问核心数据库。

## 11. 迁移优先级

```text
P0  media-ai-platform ↔ LAMICE
P0  media-platform → news-media-system
P1  Canonical Asset / Artifact
P1  Job / Event / Storage contracts
P1  Yimeng Intelligence boundary
P1  Media Processing engines
P2  UI Design System
P2  Research → Model Registry
P3  Consumer experience integration
```
