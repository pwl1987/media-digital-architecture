# Target Media Digital Ecosystem V1

## 1. 总体结构

```text
Experience Plane
  ├── Unified Portal / Shell
  ├── News Workspace
  ├── AI Studio
  ├── Creative Studio
  └── Consumer MiniApp

Business Control Plane
  └── news-media-system
      ├── Identity / RBAC
      ├── Content / Media business records
      ├── Workflow / Publish
      ├── AI Capability governance
      └── Audit / Usage

Intelligence Plane
  └── Yimeng Intelligence
      ├── Multimodal inference
      ├── Knowledge / RAG
      ├── Evidence
      ├── Embedding
      ├── Evaluation
      └── Production models

Creative Plane
  └── Creative Platform
      ├── Project / Script
      ├── Character / Location
      ├── Storyboard
      ├── Generation
      ├── Timeline
      └── Render / Export

Media Processing Plane
  ├── Shot Detection
  ├── Compression / Quality
  ├── ASR / OCR / Frame extraction
  └── Transcode / Proxy / Thumbnail

Realtime Media Plane
  ├── live-platform
  └── VBMF

Research Plane
  └── yimengjingshen / experiments
```

## 2. 主平台原则

`media-digital-platform` 是 Experience Shell，不是第二个 CMS。

它拥有：

- unified authentication / SSO integration
- global navigation
- workspace selection
- global search entry
- cross-system task center
- notification center
- module registry
- design system

它不拥有：

- Article / Media business schema
- AI Model Runtime
- Broadcast device state
- Creative generation implementation
- Research experiment runtime

## 3. 业务系统原则

`news-media-system` 作为 Content System of Record。

业务数据以它为事实源；其他系统通过 API/Event 读取或产生派生 Artifact，不直接操作其业务数据库。

## 4. Intelligence 原则

Yimeng Intelligence 不成为新的 CMS，也不重新实现企业级身份、业务权限和 AI commercial control。

它负责实际智能执行：

- text/VLM inference
- RAG
- retrieval/rerank
- evidence assembly
- multimodal analysis
- dataset/model lifecycle
- evaluation

## 5. Creative consolidation

`media-ai-platform`、`lamice`、`lamice-platform`、`ai_story`、`waoowaoo-dev` 被视为同一 Creative Video/Storytelling 领域的历史路线。

目标不是继续维护多套：

```text
Project / Task / Generation / Media / Provider / Worker
```

而是形成：

```text
Creative Platform Core
          ↑
Creative Studio
```

具体实现采用代码考古后再决定迁移顺序。

## 6. Processing consolidation

`video-shot-detection` 与 `video-compression-system` 不再定义独立业务平台；其核心价值沉淀为可调用的 Engine/Service。

标准输出必须产生 Artifact，并记录 producer/version/provenance。

## 7. Live / Broadcast separation

`live-platform` 面向流媒体运营；`VBMF` 面向广播级实时媒体 Fabric。

两者不共享业务实现，只共享上层控制语义和必要的 Media/Session references。

## 8. Domain-to-repository direction

```text
Consumer / Studio / Portal
            ↓
Business Control Plane
            ↓
Intelligence / Creative Services
            ↓
Processing Engines
            ↓
Realtime Media Runtime
            ↓
Infrastructure
```

禁止向上层反向依赖。

## 9. Migration strategy

### Wave 0 — Freeze divergence

停止新增重复平台功能；所有新能力先进行 domain ownership review。

### Wave 1 — Contract

冻结 Asset / Artifact / Job / Event / AIResult / Evidence / Identity 的跨系统契约。

### Wave 2 — Core

以 `news-media-system` 为业务基线，以 Yimeng Intelligence 为智能基线，以 VBMF/live 为媒体运行基线。

### Wave 3 — Creative

从 `media-ai-platform` / `lamice` / `lamice-platform` / `ai_story` 等抽取真正有效的 Creative assets，建立单一 Creative Platform。

### Wave 4 — Processing

统一 Shot / Compression / Transcode / ASR / OCR 等 Engine 的调用契约和 Artifact 输出。

### Wave 5 — Experience

建立统一 Portal/Shell、Design System、SSO 与 Workspace。

### Wave 6 — Legacy retirement

冻结旧系统，只保留迁移后的数据、算法、设计、协议和必要兼容层。
