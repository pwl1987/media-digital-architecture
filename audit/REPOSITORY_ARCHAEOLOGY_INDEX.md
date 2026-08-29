# Repository Archaeology Index

> 2026-08-29 · Evidence-based portfolio archaeology

## Purpose

本文件是所有纳入媒体数字智能生态的仓库考古总索引。这里的“考古”不是单纯代码审查，而是判断一个仓库：

- 实际做成了什么；
- 宣称做成了什么但没有证据；
- 哪些能力值得继承；
- 哪些设计应该避免复制；
- 未来应该继续、重建、抽取、冻结还是退役。

## Evidence Levels

| Level | Meaning |
|---|---|
| E0 | README / 文档声明，没有代码证据 |
| E1 | 源码 / 配置存在，但未证明闭环 |
| E2 | 有局部测试或可执行路径，但未证明生产闭环 |
| E3 | API + persistence + worker/runtime + test/CI 均有证据 |
| E4 | 有真实环境运行/验收/生产使用证据 |

**规则：** 不得把 E0/E1 的“功能存在”写成 Complete；核心生产能力原则上要求 E3，关键媒体/广播能力要求 E4。

## Portfolio Decisions

| Repository | Current archaeological role | Initial disposition | Priority |
|---|---|---|---|
| `news-media-system` | Business / Content Control Plane | KEEP + HARDEN | P0 |
| `YimengSpirit-Multimodal` | Intelligence Plane | REBUILD/CONTINUE UNDER CONTRACTS | P0 |
| `media-ai-platform` | Creative Platform candidate | CONSOLIDATE / REBUILD | P0 |
| `lamice` | Early Creative Studio / product branch | EXTRACT + CONSOLIDATE | P0 |
| `lamice-platform` | Python Creative Platform branch | SELECTIVE REUSE / REBUILD | P0 |
| `live-platform` | Live Operations | KEEP + ALIGN | P1 |
| `VBMF` | Broadcast Runtime/Fabric | PROTECT + IMPLEMENT | P1 |
| `video-shot-detection` | Media Processing Engine | EXTRACT / PRODUCTIZE AS ENGINE | P1 |
| `video-compression-system` | Compression / Quality Engine | EXTRACT / REBUILD SMALL | P1 |
| `ai-spider-annotation` | Data Studio candidate | REBUILD | P1 |
| `yimengjingshen` | Research Lab | KEEP AS RESEARCH | P1 |
| `xiao-opera-miniapp` | Consumer experience prototype | REBUILD EXPERIENCE | P2 |
| `media-platform` | Legacy Content Platform | FREEZE + EXTRACT | P2 |
| `city-converged-media-platform` | Earlier integrated platform | FREEZE + EXTRACT | P2 |
| `video-management-system` | Earlier video-management branch | FREEZE + EXTRACT | P2 |
| `YimengHeart` | Legacy AI compatibility | FREEZE / RETIRE | P2 |

## First Evidence-Based Findings

### `news-media-system`

The repository is no longer merely a conceptual CMS. README and package evidence show a Fastify + PostgreSQL + Drizzle backend, React 19 + Vite + Ant Design Pro frontend, BullMQ/Redis media workers, S3-compatible storage, health/readiness endpoints and multiple operational modes. However, its own README exposes operational prerequisites and configuration-sensitive paths such as queue availability and worker-role separation. Therefore its correct status is **core platform with hardening required**, not “finished product”.

### `media-platform`

This is a real early platform skeleton: 13 SQLAlchemy models, Alembic, MinIO adapter, Celery, SQLAdmin, seed data, Docker and an acceptance script are present. It also has mature-looking API envelope, pagination, business error, request ID, storage and readiness conventions. The architectural problem is not that it is useless; it is that continuing it beside `news-media-system` would recreate a second Content Platform. It should therefore be mined for patterns and migrated selectively.

### `live-platform`

It is a concrete ZLMediaKit-oriented live operations console supporting multiple ingest/playback protocols, monitoring, player integration, stream address generation and media upload. It has a genuine operational role distinct from `news-media-system`. The major debt is ecosystem divergence: React 18 + AntD 5 + Express versus the newer business baseline. This is an alignment/migration problem, not a reason to duplicate the platform.

### `video-shot-detection`

This repository has a coherent single-purpose pipeline: TransNetV2 detection, four validation signals, adaptive fusion, post-processing, export, path safety, FFmpeg timeout protection and structured audit logging. This is one of the strongest candidates for extraction as a reusable engine. It should not become another business platform.

### `video-compression-system`

The repository is a focused Python project centered on FFmpeg re-encoding and quality gating (VMAF/SSIM/PSNR). Its current tree includes application/CLI code, tests, docs, plans and OpenSpec material, but the repository metadata shows it is small and lacks production-scale platform concerns. Treat it as an engine candidate, not a system of record. The existence of multiple planning/agent files is not evidence of completeness.

### `ai-spider-annotation`

README evidence explicitly lists core data model, crawler, annotation, AI export, performance and test work as pending. This is a direct indicator of a prototype/unfinished product. Its valuable future role is Data Studio: ingest -> clean -> annotate -> review -> dataset/knowledge artifact. It should not own production user/auth/storage conventions independently.

### `yimengjingshen`

The project is fundamentally a research/teaching training stack covering pretraining, SFT, LoRA, DPO, RLAIF, tool use, agentic RL, evaluation and serving. Its correct value is research capability and model artifacts, not a production business runtime. It should produce versioned datasets, experiments and model artifacts for the Intelligence Plane.

### `xiao-opera-miniapp`

The README describes a rich consumer concept: opera/media consumption, live interaction, AI creation, activities, profile, favorites, history and social/community concepts. The implementation should not be judged by the breadth of this claim. The strongest reusable asset is product/experience intent. The future implementation should consume common platform contracts rather than build a parallel backend universe.

### `lamice` / `lamice-platform`

These repositories show multiple generations of the same creative-production idea. `lamice` documents a Next.js/React/Prisma/MySQL/Redis/BullMQ generation; `lamice-platform` documents a later FastAPI/SQLAlchemy/Vue/Element Plus plugin architecture with explicit migration gaps and known missing slices. This is exactly the pattern this archaeology effort is designed to catch: **restarting the platform under a new stack instead of consolidating the domain model first**. The decision is to preserve the best domain/workflow ideas, not to preserve all implementations.

### `media-ai-platform`

This repository has grown beyond a simple application into a platform-like creative runtime with workers, task guards, provider/capability concerns, billing, reconciliation and production-oriented infrastructure. It is the strongest candidate to become the Creative Platform Core, but only after its domain model is separated from historical implementation details and its overlap with LAMICE is collapsed.

### `VBMF`

VBMF is materially different from the unfinished application projects. Its documented architecture/runtime semantics are heavily reviewed and explicitly locked, while implementation is phased separately. Therefore it must not be classified as an abandoned prototype. The correct action is to protect the semantic baseline and finish implementation against it.

## Archaeology Rules

1. **Do not repair by default.** Every legacy project first enters evidence-driven triage.
2. **Do not inherit unverified completeness.** README badges, test counts, route counts and “LOCK FINAL” statements are evidence only for their scope.
3. **Prefer extraction over migration of accidental architecture.** Reuse algorithms, schemas, UX ideas and proven primitives; do not blindly port folder structures.
4. **One domain, one owner.** Multiple implementations may temporarily exist, but only one canonical owner is allowed per business object/capability.
5. **New work must reference the mother architecture.** Any deviation requires an ADR.
6. **Every archaeological conclusion records confidence.** A future review may overturn an E0/E1 inference when stronger evidence is found.

## Next Audit Layers

- field-level database schema comparison
- route-by-route API comparison
- task/job state machine comparison
- storage and artifact lineage comparison
- identity and authorization comparison
- frontend route/component/design comparison
- test and runtime evidence verification
- migration asset inventory at file/module level
