# Duplication Matrix — 2026-08-29 Draft

> 第一版为架构审计结论，不代表已经完成代码级证明。下一阶段将逐仓库核对实际 Schema、API、worker、frontend route 和配置。

## 1. High-risk duplication

| Capability / Domain | Repositories | Risk | Direction |
|---|---|---|---|
| AI video production | `media-ai-platform`, `LAMICE` | 🔴 Critical | Consolidate |
| Media business platform | `media-platform`, `news-media-system` | 🔴 Critical | Migrate → news-media |
| Project model | `news-media`, `media-ai`, `LAMICE`, legacy media platform | 🔴 High | Canonicalize by domain |
| Asset / media object | Multiple repositories | 🔴 High | Canonical Asset + Artifact |
| Async Job | Celery / BullMQ / custom runtimes | 🟠 Medium | Contract unify, runtime separate |
| Storage abstraction | Multiple repositories | 🟠 High | Common Storage Contract |
| AI provider/model configuration | Yimeng AI / media AI / creative systems | 🔴 High | Central Capability/Model contract |
| Frontend design system | React/AntD/Next/Tailwind/Gradio/Solara | 🔴 High UX risk | Shared design language |
| Shot detection | dedicated engine + product-level needs | 🟠 Medium | Engine ownership |
| Compression/QC | dedicated engine + media workflows | 🟠 Medium | Engine ownership |
| Live streaming | `live-platform`, `news-media` | 🟠 Medium | Live API boundary |
| Broadcast runtime | `VBMF` + upper platforms | 🟠 Boundary risk | Control API only |
| Research model code | `yimengjingshen` + production AI | 🔴 High | Artifact boundary |

## 2. Stack duplication observed

### Backend

- FastAPI / Express / Fastify / Next.js server routes
- SQLAlchemy / Prisma / Drizzle
- PostgreSQL / MySQL / SQLite
- Celery / BullMQ / custom runtime

### Frontend

- React 18
- React 19
- Vite
- Next.js
- Ant Design
- Ant Design Pro
- Tailwind
- Gradio
- Solara

技术多样性本身不是问题；没有统一边界才是问题。

## 3. Critical semantic collisions

### `Project`

可能表示内容项目、AI 创作项目、广播项目或研究实验。不能继续作为无上下文的跨域公共语义。

### `Shot`

至少需要区分 `VideoShot` 与 `StoryboardShot`。

### `Clip`

至少需要区分媒体素材片段和时间线编辑片段。

### `Media / Asset / File / Artifact`

当前生态需要建立明确关系，不能让 URL/file path 成为事实源。

## 4. Most dangerous future failure mode

如果继续各仓库独立扩展，预计会出现：

```text
Product A → Asset A → Job A → Provider A
Product B → Asset B → Job B → Provider B
Product C → Asset C → Job C → Provider C
```

最终“融合”会退化为 ETL 和适配器堆积。

正确方向：

```text
Canonical Domain Objects
        ↓
Cross-System Contracts
        ↓
Specialized Implementations
```
