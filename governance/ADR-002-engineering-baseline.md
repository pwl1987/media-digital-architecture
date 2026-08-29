# ADR-002 — Engineering Baseline

- Status: PROPOSED
- Date: 2026-08-29
- Scope: all new production projects in the ecosystem

## Decision

统一的是开发基线、契约和工程体验；专业 runtime 保持技术自治。

### Production Web / Business UI

Preferred baseline:

- TypeScript
- React 19
- Vite for SPA / Next.js only where SSR or app routing is justified
- Ant Design 6 for enterprise interfaces
- Playwright
- Vitest
- pnpm

`news-media-system` 当前已经具备 React 19 + Vite + Ant Design 6、共享 package 的基础，可作为第一候选基线。

### Business Backend

Preferred baseline:

- Node.js 24+
- TypeScript
- Fastify
- PostgreSQL
- Drizzle
- BullMQ
- Valkey/Redis-compatible runtime
- S3-compatible object storage
- OpenTelemetry

### AI / Intelligence

Preferred baseline:

- Python 3.12
- FastAPI
- PyTorch
- Transformers
- vLLM / SGLang where production serving benefits
- PostgreSQL + pgvector where suitable
- S3-compatible artifact storage
- OpenTelemetry

### Media / Broadcast Runtime

Professional stack is intentionally exempt from the business stack:

- Rust where realtime correctness and systems integration require it
- GStreamer / FFmpeg
- DeckLink / SDI / IP media protocols
- SRT / RIST / RTP as appropriate
- ZLMediaKit for streaming operations where appropriate

## Explicitly allowed exceptions

- WeChat Mini Program native runtime
- Gradio / Solara for research and model experiments
- Python-specialized engines
- Rust realtime engines
- Existing legacy systems during migration

Exceptions must declare their boundary and consumer-facing contract.

## Rules

1. New production frontend should not introduce Vue or another component framework without ADR.
2. New business backend should not introduce a second ORM/database paradigm without ADR.
3. New AI product should not invent another provider registry if it can consume the canonical capability/model contract.
4. New media engine should expose Job/Artifact semantics rather than UI-specific behavior.
5. A project may use a different runtime internally, but it must not leak runtime-specific types into cross-system contracts.
6. Every production service must declare owner, role, dependencies, storage, events and health model.

## Rationale

The current ecosystem already contains React/AntD, Vue/Element Plus, Solara, Gradio, Next.js/Tailwind and multiple backend stacks. Removing all diversity is unnecessary; uncontrolled divergence is the actual problem.
