# Target Architecture V1 — Draft

## 1. 目标

建立一个由多个专业系统组成、但共享统一领域语言和跨系统契约的媒体数字智能生态。

目标不是 Monolith，而是：

> **One Architecture, Multiple Specialized Systems.**

## 2. 平面模型

### Experience Plane

面向最终用户和业务人员：

- News Web / Portal
- AI Creative Studio
- Yimeng Culture MiniApp
- 专业运营工作台

Experience 不直接依赖底层媒体设备、数据库或模型 runtime。

### Business Control Plane

主要由 `news-media-system` 承担：

- User / Organization / Site
- Content
- Media Asset registration
- Workflow
- Publication
- Business permissions
- AI capability governance
- Cross-system orchestration

它是业务事实源，而不是所有底层计算的实现者。

### Intelligence Plane

主要由 `YimengSpirit-Multimodal` 及相关 AI services 承担：

- LLM / VLM
- RAG
- Knowledge
- Evidence
- Embedding
- Evaluation
- Model serving abstraction
- AI capability execution

### Media Processing Plane

由专业 Engine 组成：

- `video-shot-detection`
- `video-compression-system`
- future ASR / OCR / subtitle / thumbnail / transcode engines

这些系统消费 Artifact，产生新的 Artifact，并通过 Job/Event Contract 报告生命周期。

### Realtime Media Plane

- `live-platform` — streaming operations
- `VBMF` — broadcast-grade realtime media fabric

Realtime Media Plane 不被普通 CRUD/async-job 业务模型绑架。

### Infrastructure Plane

提供：

- PostgreSQL / MySQL where appropriate
- Object Storage / S3-compatible storage
- Redis/Valkey where appropriate
- GPU runtime
- FFmpeg / GStreamer
- DeckLink / SDI / IP media runtime
- Observability

## 3. 依赖方向

```text
Experience
    ↓
Business Control
    ↓
Intelligence / Processing / Live Control
    ↓
Runtime
    ↓
Infrastructure
```

允许上层调用下层 Contract；禁止底层反向依赖上层业务实现。

示例：

- `news-media-system` → Live API：允许
- `news-media-system` → VBMF Control API：允许
- `news-media-system` → Shot Detection Job：允许
- `LAMICE` → Intelligence API：允许
- `LAMICE` → DeckLink SDK：禁止
- Shot Engine → News UI：禁止
- VBMF → React component：禁止

## 4. 专业系统归位

| 系统 | 目标角色 | 状态 |
|---|---|---|
| news-media-system | Content / Business Platform | Core |
| YimengSpirit-Multimodal | Intelligence Platform | Core |
| VBMF | Broadcast Media Fabric | Core |
| live-platform | Live Operations | Core |
| video-shot-detection | Shot Detection Engine | Engine |
| video-compression-system | Compression / Quality Engine | Engine |
| media-ai-platform | AI Video Production Platform | Consolidate |
| LAMICE | Creative Studio | Consolidate |
| ai-spider-annotation | Data Studio | Supporting |
| yimengjingshen | Model Research Lab | Research |
| xiao-opera-miniapp | Consumer Experience | Application |
| media-platform | Legacy / Migration Source | Retire |
| YimengHeart | Legacy Compatibility | Retire |

## 5. AI Video Production 的目标关系

`media-ai-platform` 与 `LAMICE` 当前高度重叠，不应继续复制开发。

目标：

```text
AI Video Production Platform
├── Project / Creative domain
├── Script
├── Storyboard
├── Character / Scene
├── Timeline
├── Generation orchestration
├── Voice / Music
├── Rendering / Composition
└── Artifact lifecycle
          ↑
     LAMICE Studio
```

LAMICE 更适合作为 Creative Studio，而平台承担业务编排、资产、任务和 AI capability。

## 6. 媒体处理目标

```text
Media Asset
    ↓
Processing Job
    ↓
Specialized Engine
    ↓
Artifact(s)
    ↓
Event
    ↓
Asset/Knowledge enrichment
```

引擎可以独立部署、独立扩展、独立使用 GPU/CPU；上层不依赖其内部实现。

## 7. Broadcast / Live 边界

```text
Live Operations
    ↓
Session / Stream / Channel API
    ↓
live-platform

Broadcast Control
    ↓
Broadcast Session / Source / Health / Switch API
    ↓
VBMF
```

`VBMF` 不应变成普通 Web 后端；`live-platform` 也不应侵入广播设备和 Fabric 内部实现。

## 8. 最终形态

```text
                    EXPERIENCE
                         │
          ┌──────────────┴──────────────┐
          │                             │
    Business Apps                 Creative Apps
          │                             │
          └──────────────┬──────────────┘
                         ▼
               BUSINESS CONTROL PLANE
                news-media-system
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
    INTELLIGENCE     PROCESSING      REALTIME
     Yimeng AI       Media Engines   Live / VBMF
          │              │              │
          └──────────────┼──────────────┘
                         ▼
                    INFRASTRUCTURE
```
