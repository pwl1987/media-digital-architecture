# Media Digital Architecture

> 多媒体数字化与 AI 生态母架构（Architecture Source of Truth）

本仓库不是业务运行时，也不是把所有项目合并成一个“大单体”。它用于定义 `pwl1987` 媒体、融媒体、直播、广播、AI、多模态知识、AI 视频生产与研究项目之间的共同架构原则、领域对象、跨系统契约、依赖方向、生命周期与迁移路线。

## 当前阶段

**Architecture Baseline: Pre-Freeze / DRAFT-0.2**

当前工作重点已经从“画目标架构”进入：

```text
Portfolio Discovery
  ↓
Repository Archaeology
  ↓
Evidence Verification
  ↓
Domain / Contract Normalization
  ↓
Recovery / Rebuild / Extract / Freeze / Retire
  ↓
Target Platform Implementation
```

核心原则：**不以代码数量、README 功能清单、测试数量或“已完成”标记判断项目是否成熟。** 必须区分声明、实现、集成、验证与真实运行证据。

## 当前纳入审计的项目族谱

### 核心平台/运行时

- `news-media-system` — 融媒体业务主平台 / Content & Business Control Plane
- `YimengSpirit-Multimodal` — 沂蒙领域 AI / Intelligence Plane
- `live-platform` — 直播运营 / Live Operations
- `VBMF` — 广播级 IP Media Fabric / Realtime Broadcast Runtime
- `media-ai-platform` — Creative Platform candidate
- `lamice` — Creative Studio generation lineage
- `lamice-platform` — Creative Platform alternate lineage

### 能力引擎 / 数据 / 研究

- `video-shot-detection` — 视频镜头检测 Engine
- `video-compression-system` — 压缩与质量门禁 Engine
- `ai-spider-annotation` — Data Studio candidate
- `yimengjingshen` — Research / Training Lab

### 产品体验

- `xiao-opera-miniapp` — 公众文化消费端

### 历史 / 迁移来源

- `media-platform`
- `city-converged-media-platform`
- `video-management-system`
- `YimengHeart`

### 进一步发现的相关谱系 / 参考

- `ai_story` — AI story-video workflow reference/history
- `waoowaoo-dev` — AI video studio reference/history
- `aigcpanel` — local model runtime packaging reference
- `flow-kit` — media/workflow related asset; requires deeper audit
- `rm-contest-writer` — content production related asset; requires deeper audit
- `CCTVVideoDownloader` — acquisition tool; currently outside core platform boundary
- `WebAV` / `QuickCut` / `CutClaw` — media editing reference candidates
- `openreel-video` — external browser editor benchmark
- `media-source-extract` — external upstream fork/reference, not assumed proprietary core asset

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
9. 老项目是应该继续修、重建、抽取还是冻结？
10. 自研代码、fork、外部参考之间的 provenance 如何证明？

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

## 核心产品策略

### 一个体验

通过未来的 `media-digital-platform` 统一：

- Identity / SSO
- Navigation
- Workspace
- Global Search
- Task Center
- Notification
- Design System
- Module Registry

### 一套领域语言

跨仓库统一：

- Asset
- Artifact
- Job
- Task
- Generation
- Evidence
- Knowledge
- Dataset
- Model
- Session

### 多套专业运行时

专业技术可以保留：

- Business Web / Backend：TypeScript / React / Fastify / PostgreSQL
- AI：Python / FastAPI / PyTorch / Transformers / vLLM/SGLang
- Media Runtime：Rust / GStreamer / FFmpeg / DeckLink
- Live：ZLMediaKit / SRT / RTP / WebRTC
- Consumer：WeChat MiniApp

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
- **旧项目不自动继承。** 老项目默认进入考古，不默认进入开发 backlog。
- **外部 provenance 必须明确。** Fork/参考项目不能直接算自有资产。

## 文档入口

### Architecture

- [`architecture/TARGET_ARCHITECTURE_V1.md`](architecture/TARGET_ARCHITECTURE_V1.md)
- [`architecture/TARGET_PRODUCT_STRUCTURE.md`](architecture/TARGET_PRODUCT_STRUCTURE.md)
- [`architecture/TECHNICAL_ARCHITECTURE.md`](architecture/TECHNICAL_ARCHITECTURE.md)
- [`architecture/PLATFORM_BOUNDARIES_V1.md`](architecture/PLATFORM_BOUNDARIES_V1.md)

### Domain / Contracts

- [`domains/DOMAIN_MODEL.md`](domains/DOMAIN_MODEL.md)
- [`objects/CANONICAL_OBJECTS.md`](objects/CANONICAL_OBJECTS.md)
- [`contracts/CONTRACTS.md`](contracts/CONTRACTS.md)

### Governance

- [`governance/REPO_ROLES.md`](governance/REPO_ROLES.md)
- [`governance/ARCHAEOLOGY_METHOD.md`](governance/ARCHAEOLOGY_METHOD.md)
- [`governance/LEGACY_AND_INCOMPLETE_POLICY.md`](governance/LEGACY_AND_INCOMPLETE_POLICY.md)
- [`governance/RECOVERY_FIRST_ROADMAP.md`](governance/RECOVERY_FIRST_ROADMAP.md)
- [`governance/PROJECT_COMPLETION_GATE.md`](governance/PROJECT_COMPLETION_GATE.md)
- [`governance/ASSET_PROVENANCE_POLICY.md`](governance/ASSET_PROVENANCE_POLICY.md)

### Audit

- [`audit/REPOSITORY_ARCHAEOLOGY_INDEX.md`](audit/REPOSITORY_ARCHAEOLOGY_INDEX.md)
- [`audit/REPOSITORY_PORTFOLIO_REGISTER.md`](audit/REPOSITORY_PORTFOLIO_REGISTER.md)
- [`audit/REPOSITORY_HEALTH_REGISTER.md`](audit/REPOSITORY_HEALTH_REGISTER.md)
- [`audit/TECH_FACT_MATRIX.md`](audit/TECH_FACT_MATRIX.md)
- [`audit/DUPLICATION_MATRIX.md`](audit/DUPLICATION_MATRIX.md)
- [`audit/MIGRATION_MAP.md`](audit/MIGRATION_MAP.md)
- [`audit/PORTFOLIO_LINEAGE.md`](audit/PORTFOLIO_LINEAGE.md)
- [`audit/2026-08-29-ecosystem-audit.md`](audit/2026-08-29-ecosystem-audit.md)

## 工作方式

后续所有项目都遵守：

```text
先考古 → 再定性 → 再确定 owner → 再确定迁移目标 → 最后才编码
```

任何新能力如果已经存在于其他仓库，必须先证明：

- 当前 canonical owner 是谁；
- 是否已有可复用实现；
- 为什么不能通过 Contract 复用；
- 为什么不能 Extract / Rebuild；
- 新增 Runtime 是否真的必要。

## 状态

**Architecture Baseline: DRAFT-0.2 / Pre-Freeze**

当前仍不冻结全部实现细节。后续将继续对数据库 Schema、API、Job、Storage、Auth、UI 路由、测试、运行证据以及文件/模块级迁移目标进行逐项交叉审计，并把更强证据持续回写到本仓库。