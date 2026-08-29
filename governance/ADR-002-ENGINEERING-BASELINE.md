# ADR-002 — Ecosystem Engineering Baseline

- Status: Proposed
- Date: 2026-08-29
- Scope: ecosystem-wide production systems

## Decision

新建设的生产系统默认采用以下技术基线；现有系统不要求立即重写，但进入重大版本、功能重构或迁移时，应优先向该基线收敛。

## Web

Default:

- TypeScript
- React 19
- Ant Design 6
- Vite for SPA
- Next.js only where SSR/app-router is justified
- pnpm
- Vitest
- Playwright

## Business Backend

Default:

- Node.js 24 LTS/current approved runtime
- TypeScript
- Fastify
- PostgreSQL
- Drizzle ORM
- BullMQ
- Valkey/Redis-compatible cache and queue backend
- S3-compatible object storage
- OpenTelemetry

## AI / ML

Default:

- Python 3.12
- FastAPI
- PyTorch
- Transformers
- vLLM/SGLang where serving requirements justify them
- PostgreSQL + pgvector for knowledge/retrieval where appropriate
- S3-compatible object storage
- OpenTelemetry

## Media Runtime

Specialized baseline:

- Rust where realtime/control correctness benefits from systems-level guarantees
- GStreamer
- FFmpeg
- DeckLink/SDI/IP media APIs
- SRT/RIST/RTP where required

## Live Runtime

Specialized baseline:

- ZLMediaKit or an explicitly approved equivalent
- SRT/RTMP/WebRTC as appropriate

## Non-goals

本 ADR 不要求所有项目：

- 使用同一语言
- 使用同一数据库
- 使用同一消息队列实现
- 使用同一 Web framework
- 使用同一部署方式
- 使用同一模型 runtime

## Mandatory engineering contracts

无论采用何种技术栈，都必须遵循生态级：

- identity rules
- API contract
- event semantics
- Job/Task semantics
- Asset/Artifact provenance
- auth propagation
- observability fields
- versioning
- security baseline
- design system

## Exception process

技术偏离必须在对应仓库的 ADR 中说明：

1. 为什么基线不适用。
2. 为什么替代技术更优。
3. 增加了什么运维/人才/依赖成本。
4. 如何保持生态 Contract 兼容。
5. 退出或迁移条件是什么。

“个人偏好”“这个框架更流行”“已经写了一点”不足以构成偏离理由。
