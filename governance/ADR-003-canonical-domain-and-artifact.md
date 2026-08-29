# ADR-003 — Canonical Domain Objects and Artifact Lineage

- Status: PROPOSED
- Date: 2026-08-29

## Decision

整个生态采用统一的领域语言，但由各专业系统拥有各自领域对象的事实源。

## Canonical objects

### Identity / Business

- Organization
- User
- Site
- ContentProject
- Content

### Media / Asset

- Asset — 可管理的原始或业务资产
- Artifact — 某次处理、分析、生成产生的具体产物
- Media — Asset/Artifact 的媒体语义

### Runtime

- Session
- Job
- Event

### Intelligence

- Knowledge
- Evidence
- Dataset
- Model
- Generation

## Domain-qualified objects

不得跨域使用语义模糊的裸对象名：

- `VideoShot` — 现实视频镜头分析结果
- `StoryboardShot` — 创作分镜镜头
- `StoryboardPanel` — 分镜/漫剧画面单元
- `TimelineClip` — 编辑时间线片段
- `BroadcastSession` — 广播运行会话
- `ResearchExperiment` — 研究实验
- `CreativeProject` — AI 创作项目

## Identity rules

- Business ID != storage URL
- `artifact_id` 不因对象存储搬迁而改变
- URL / storageKey / bucket 都是 locator
- 产物必须记录 producer、version、checksum、inputs/provenance
- 一个源 Asset 可以派生多个 Artifact
- 一个 Artifact 可以被多个下游系统引用，但不能被复制成语义相同的“第二事实源”

## Canonical lineage

```text
Source / Content Asset
        ↓
Derived Artifact
        ↓
Analysis / Knowledge Artifact
        ↓
Dataset Sample
        ↓
Model Artifact
        ↓
Generation / Business Result
```

## Ownership

`news-media-system` owns business Content and business Asset registration.

Intelligence systems own Knowledge/Evidence and model-oriented artifacts.

Creative platform owns CreativeProject and production workflow state.

Realtime platforms own Session/Broadcast state.

Processing engines own their execution details but must not become the business System of Record.

## Non-goals

本 ADR 不要求所有系统共享同一物理数据库，也不要求所有领域对象进入同一 ORM schema。

后续 Schema Audit 必须把上述语义映射到每个仓库当前实际表/模型，并给出 migrate/freeze/alias 决策。
