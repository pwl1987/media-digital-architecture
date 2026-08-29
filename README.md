# Media Digital Architecture

> 多媒体数字化与 AI 生态母架构（Architecture Source of Truth）

本仓库不是业务运行时，也不是把所有项目合并成一个“大单体”。它用于定义 `pwl1987` 媒体、融媒体、直播、广播、AI、多模态知识、AI 视频生产与研究项目之间的**共同架构原则、领域对象、跨系统契约、依赖方向、生命周期与迁移路线**。

## 当前纳入审计的项目

- `news-media-system` — 融媒体业务主平台 / Content & Business Control Plane
- `YimengSpirit-Multimodal` — 沂蒙领域 AI / Intelligence Plane
- `VBMF` — 广播级 IP Media Fabric / Realtime Broadcast Runtime
- `live-platform` — 直播运营平台 / Live Operations
- `media-platform` — 旧一代融媒体后端骨架 / Migration Source
- `video-shot-detection` — 视频镜头检测引擎
- `video-compression-system` — 视频压缩与质量门禁引擎
- `media-ai-platform` — AI 视频生产平台
- `lamice` — AI 漫剧/短剧创作工作台候选产品前端/应用层
- `ai-spider-annotation` — 数据采集与标注工作台
- `yimengjingshen` — 模型研究与训练实验室
- `xiao-opera-miniapp` — 公众文化消费端
- `YimengHeart` — 历史 AI 问答 / Legacy Compatibility

## 母架构核心判断

当前最大问题不是“技术栈太多”，而是多个仓库对以下问题存在不同答案：

1. 什么是业务系统，什么是底层引擎？
2. 谁拥有用户、内容、媒体资产、知识、任务和模型的最终事实？
3. AI Control Plane 与 AI Data Plane 谁负责什么？
4. URL、File、Media、Asset、Artifact 哪个才是资产身份？
5. Project / Shot / Clip / Panel / Episode 等对象是否拥有统一语义？
6. Queue 技术是否需要统一，还是只统一 Job Contract？
7. 前端是否必须同一技术栈，还是应该统一 Design System？
8. 研究代码与生产模型的边界在哪里？

本仓库的目标是先解决这些边界，再推进下一轮跨仓库实现。

## 目标分层

```text
Experience Plane
  Web / Portal / MiniApp / Studio
        ↓
Business Control Plane
  news-media-system
  User / Site / Content / Workflow / Publish / AI Governance
        ↓
Intelligence Plane
  Yimeng Intelligence
  LLM / VLM / RAG / Knowledge / Evidence / Evaluation
        ↓
Media Processing Plane
  Shot Detection / Compression / ASR / OCR / Transcode / QC
        ↓
Realtime Media Plane
  live-platform / VBMF
        ↓
Infrastructure
  Storage / GPU / Network / Runtime
```

## 核心资产链

```text
ContentAsset
    ↓
Artifact
    ↓
KnowledgeArtifact
    ↓
DatasetSample
    ↓
ModelArtifact
```

## 核心原则

- **统一逻辑，不强制物理统一。** 不要求所有项目使用同一语言、数据库或 Queue；要求遵守共同领域模型和跨系统契约。
- **业务平面与智能平面分离。** `news-media-system` 管业务控制，Yimeng AI 管智能执行。
- **控制面与数据面分离。** AI capability、provider、quota、audit 等控制能力与实际模型 runtime 分开。
- **资产身份独立于访问 URL。** URL 是 locator，不是 identity。
- **研究与生产分离。** `yimengjingshen` 的实验代码不能直接成为生产运行时依赖。
- **引擎能力复用，不复制业务系统。** Shot Detection、Compression 等应成为能力服务，而不是多个产品各自重写。
- **实时媒体与离线 Job 分离。** VBMF 的 realtime semantics 不强行套入普通异步任务模型。
- **Evidence 是知识产品的一等公民。** 对历史文化领域，可信来源、证据和可追溯性优先于单纯生成效果。
- **实验 UI 不升级为生产 UI。** Gradio/Solara 可以服务研发验证，但正式产品采用正式前端体系。

## 文档入口

- [`architecture/TARGET_ARCHITECTURE_V1.md`](architecture/TARGET_ARCHITECTURE_V1.md) — 目标总体架构
- [`architecture/TECHNICAL_ARCHITECTURE.md`](architecture/TECHNICAL_ARCHITECTURE.md) — 技术架构原则
- [`domains/DOMAIN_MODEL.md`](domains/DOMAIN_MODEL.md) — 领域模型
- [`objects/CANONICAL_OBJECTS.md`](objects/CANONICAL_OBJECTS.md) — Canonical Objects
- [`contracts/CONTRACTS.md`](contracts/CONTRACTS.md) — 跨系统契约总览
- [`governance/REPO_ROLES.md`](governance/REPO_ROLES.md) — 仓库角色与生命周期
- [`audit/DUPLICATION_MATRIX.md`](audit/DUPLICATION_MATRIX.md) — 重复能力审计
- [`audit/MIGRATION_MAP.md`](audit/MIGRATION_MAP.md) — 初步迁移路线
- [`audit/2026-08-29-ecosystem-audit.md`](audit/2026-08-29-ecosystem-audit.md) — 本轮审计基线

## 状态

**Architecture Baseline: DRAFT-0.1**

当前阶段只冻结原则、边界和事实；不冻结具体实现选型的全部细节。后续将继续对数据库 Schema、API、Job、Storage、Auth、UI 路由和实际代码进行逐项交叉审计，审计结果再升级为 V1.0。