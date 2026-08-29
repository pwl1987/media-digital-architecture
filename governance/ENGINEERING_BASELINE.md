# Unified Engineering Baseline — Draft 0.1

## 1. Rule

统一工程基线的目的，是让新项目和重建项目默认走同一套工程语言；不是强迫专业运行时迁移到同一技术栈。

## 2. Production Web baseline

Preferred:

- TypeScript
- React 19
- Ant Design 6
- Vite for SPA
- Next.js only when SSR/SEO/app-router has a concrete requirement
- pnpm
- Vitest
- Playwright

Existing React applications on older versions may migrate incrementally. New feature work must not introduce another UI framework without ADR approval.

## 3. Business backend baseline

Preferred:

- Node.js 24 LTS-class runtime baseline
- TypeScript
- Fastify
- PostgreSQL
- Drizzle ORM
- BullMQ
- Valkey/Redis-compatible runtime
- S3-compatible object storage
- OpenTelemetry

Express/other frameworks may remain in legacy applications but should not become the default for new business services.

## 4. AI baseline

Preferred:

- Python 3.12
- FastAPI for service boundary
- PyTorch
- Transformers
- vLLM/SGLang where appropriate for serving
- PostgreSQL + pgvector for relational/semantic knowledge where appropriate
- S3-compatible storage
- OpenTelemetry

AI research projects can diverge; production AI services require a stable API boundary and artifact/version identity.

## 5. Media runtime baseline

Preferred:

- FFmpeg
- GStreamer where graph/runtime control is needed
- Rust where realtime or systems-level control is required
- DeckLink/SDI/IP media runtime for broadcast workloads
- SRT/RIST/RTP according to workload

Broadcast/realtime code must not be rewritten merely to achieve language uniformity.

## 6. Database policy

- PostgreSQL is the default relational database for new business/knowledge systems.
- MySQL/Prisma in existing Creative systems is a migration target, not an immediate rewrite mandate.
- Each service owns its schema.
- Cross-service data uses API/Event/Artifact contracts.
- Direct cross-database reads are forbidden.

## 7. Queue policy

BullMQ/Valkey is the default for ordinary asynchronous business workloads.

Other systems may use Celery or specialized runtime scheduling when justified.

The technology is not the contract. The contract is:

```text
Task → Job → Attempt → Result/Artifact
```

with common lifecycle semantics.

## 8. Object storage policy

All generated or uploaded bytes must be represented by an Artifact/Asset identity. A URL is never the canonical identity.

Required metadata should include:

- artifact_id
- media_type
- size
- checksum
- storage_locator
- producer
- producer_version
- created_at
- provenance

## 9. API engineering policy

Every cross-system API must define:

- version
- authentication context
- request schema
- response schema
- error schema
- idempotency behavior
- timeout/retry semantics
- pagination where relevant
- trace/request correlation

ORM models must not be exposed as public API contracts.

## 10. Error model

Errors should distinguish at minimum:

```text
validation
authentication
authorization
not_found
conflict
rate_limited
dependency_unavailable
timeout
processing_failed
internal
```

The exact HTTP mapping may vary, but semantic categories must remain stable.

## 11. Observability

Cross-system requests and jobs should carry, where applicable:

```text
trace_id
request_id
job_id
task_id
artifact_id
actor_id
organization_id
producer
producer_version
status
error_code
latency_ms
```

## 12. New project gate

A new production repository must declare:

```text
role
owned domains
provided capabilities
consumed contracts
owned data
runtime
storage
job system
observability
security baseline
```

Deviation from this baseline requires an ADR in `media-digital-architecture`.
