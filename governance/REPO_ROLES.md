# Repository Roles & Lifecycle — Draft 0.1

## 1. Role taxonomy

- **Platform** — 业务或控制面的长期核心系统。
- **Engine** — 可被多个系统调用的专业能力。
- **Runtime/Fabric** — 实时媒体或基础运行时。
- **Studio/Application** — 面向用户的具体产品体验。
- **Lab** — 研究、训练、实验。
- **Legacy** — 兼容、迁移来源，不再扩张核心职责。

## 2. Current assignments

| Repository | Role | Decision |
|---|---|---|
| `news-media-system` | Platform | Core System of Record |
| `YimengSpirit-Multimodal` | Intelligence Platform | Core |
| `VBMF` | Runtime/Fabric | Core |
| `live-platform` | Platform | Core Live Operations |
| `video-shot-detection` | Engine | Extract / standardize capability |
| `video-compression-system` | Engine | Extract / standardize capability |
| `media-ai-platform` | Platform | Consolidate creative backend/orchestration |
| `LAMICE` | Studio/Application | Consolidate as Creative Studio |
| `ai-spider-annotation` | Studio/Application | Data Studio |
| `yimengjingshen` | Lab | Research only |
| `xiao-opera-miniapp` | Application | Consumer Experience |
| `media-platform` | Legacy | Freeze and migrate useful assets |
| `YimengHeart` | Legacy | Compatibility then retire |

## 3. Lifecycle states

```text
PROPOSED
   ↓
ACTIVE
   ↓
CONSOLIDATING
   ↓
FROZEN
   ↓
LEGACY
   ↓
RETIRED
```

A repository must not silently change role. Role changes require an Architecture Decision Record.

## 4. Ownership rules

A capability should have one canonical owner. Other repositories consume it through contract.

Examples:

- Shot detection → `video-shot-detection` / future Media Processing owner.
- Compression quality gate → `video-compression-system` / future Media Processing owner.
- Content business state → `news-media-system`.
- Historical knowledge → Yimeng Intelligence.
- Broadcast realtime control → `VBMF`.
- Live streaming operations → `live-platform`.
- AI creative orchestration → `media-ai-platform`.
- Creative UX → `LAMICE`.

## 5. Anti-patterns

禁止：

- 两个 Platform 同时成为同一业务域的事实源。
- Engine 直接依赖业务 UI。
- UI 直接访问另一个系统的数据库。
- 业务系统直接调用 DeckLink/GStreamer/FFmpeg 内部实现而绕过 runtime contract。
- Research Lab 成为生产服务的源码依赖。
- 复制同一 AI provider registry 到多个产品。
- 复制同一 Asset/Artifact/Job 模型并声称“以后再统一”。

## 6. Consolidation priority

### P0

`LAMICE` ↔ `media-ai-platform`

消除双 Creative Project、双 Generation、双 Media/Artifact、双 Job/Provider 体系。

### P0

`media-platform` → `news-media-system`

停止继续建设第二套融媒体主平台；迁移可复用领域知识与基础设施设计。

### P1

`video-shot-detection` + `video-compression-system`

统一进入 Media Processing Contract，但保持 Engine 独立部署能力。

### P1

`live-platform` ↔ `VBMF`

统一控制语义和上层集成，不合并实时运行时。

### P1

`yimengjingshen` → Model Artifact / Dataset / Evaluation 与生产 Intelligence 解耦。

## 7. Change control

任何新仓库、新 Platform、新一级 Domain Object、新跨系统 API 都应先进入本仓库审查。
