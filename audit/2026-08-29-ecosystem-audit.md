# Ecosystem Audit — 2026-08-29

## Executive conclusion

当前项目群的主要矛盾不是单仓库工程质量，而是多个项目在不同时间形成了重叠的产品边界、对象模型、任务模型、AI Provider 模型、资产模型和 UI 体系。

如果继续逐仓库增加功能而不建立母架构，未来融合成本会显著上升。

## Major findings

### A. Platform duplication

`media-platform` 与 `news-media-system` 都承担融媒体业务后端职责。后者应成为长期业务事实源，前者进入迁移/冻结路线。

### B. Creative platform duplication

`media-ai-platform` 与 `LAMICE` 在技术栈和产品域上高度重叠：Next.js/React、Prisma/MySQL、Redis/BullMQ，以及 AI 视频创作、项目、分镜、媒体和生成任务等概念。两者需要形成 Platform + Studio 关系，而不是继续并行复制。

### C. Realtime boundary

`live-platform` 与 `VBMF` 均属于实时媒体领域，但抽象层级不同。前者是流媒体运营，后者是广播级媒体 Fabric。应统一控制语义，不应合并运行时。

### D. Processing engines

`video-shot-detection` 和 `video-compression-system` 已经具备独立专业引擎特征。应通过标准 Job/Artifact Contract 被多个上层系统复用。

### E. Research/production boundary

`yimengjingshen` 应保持研究实验室定位。生产系统消费 Model Artifact，而不是依赖研究代码。

### F. Asset model risk

多个项目出现 File / URL / Media / Asset / Artifact 等不同叫法。尤其 AI 创作平台出现 imageUrl/videoUrl 等直接 locator 字段，与更成熟的 MediaObject/Asset 思路存在潜在冲突。

生产级生态必须让身份与 locator 解耦，并保留 provenance。

### G. Job model risk

Celery、BullMQ、专用 realtime runtime 可以共存；真正需要统一的是 Job 的生命周期和输入/输出语义，而不是 Queue 技术。

### H. UI fragmentation

React 18/19、Vite、Next.js、Ant Design、Ant Design Pro、Tailwind、Gradio、Solara 等并存。技术栈多样性不是核心问题；Design Token、状态模型、信息架构和核心交互模式没有母规范才是问题。

## Current architecture scorecard

| Dimension | Status |
|---|---|
| Technical capability | Strong |
| Engineering capability | Strong / improving |
| Product breadth | Strong |
| Architecture consistency | Weak |
| Domain model consistency | Weak |
| API consistency | Weak |
| Asset/artifact model | High risk |
| Job model | Medium-high risk |
| UI consistency | High risk |
| Product boundary | High risk |
| Lifecycle governance | Weak |

## Audit principle

本文件是第一版架构审计记录，不把推断冒充代码事实。下一阶段必须针对每个仓库进行 code-level verification：

1. Repository tree
2. Runtime entrypoints
3. Database schema
4. API routes and DTOs
5. Authentication/authorization
6. Queue/worker implementation
7. Object storage access
8. Asset/Artifact entities
9. AI provider/model registry
10. Frontend routes/components
11. Docker/deployment
12. Observability
13. Tests and CI

## Next gate

只有完成上述 code-level verification，才能冻结 Canonical Object Schema、OpenAPI/AsyncAPI、Migration Plan 和正式 Architecture V1.0。
