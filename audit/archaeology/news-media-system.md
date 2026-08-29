# Archaeology — `news-media-system`

## Verdict

**KEEP / CORE / P0**, but do not treat as complete. It is the best current candidate for the Business Control Plane and Content System of Record.

## What is demonstrably present

README evidence shows a frontend/backend monorepo with `backend/` using Fastify + PostgreSQL + Drizzle and `frontend/` using React 19 + Vite + Ant Design Pro. Media processing uses BullMQ/ioredis and FFmpeg; the documented standard deployment separates worker roles for media/trim/AI/scheduler and includes PostgreSQL, Valkey, MinIO/S3, frontend and optional SRS/worker services. It exposes health/readiness conventions and documents production-sensitive secrets. [E2 baseline from current repository evidence]

## Architectural value to preserve

- Business content ownership
- Site / article / media workflow model
- AI capability/provider governance
- Business-level job orchestration
- React 19 + Vite + Ant Design 6 direction
- Fastify + PostgreSQL + Drizzle business backend baseline
- Existing shared UI/type packages as candidates for refinement

## Risks found

1. The system has enough subsystems that “core business platform” can expand into a giant monolith.
2. Worker-role/profile logic is operationally sensitive; a wrong role configuration can cause duplicate queue consumption.
3. AI governance is valuable, but must remain control-plane logic rather than becoming the model runtime.
4. Existing media processing and live integrations must remain adapters/service boundaries rather than leaking runtime implementation into business code.

## Completion interpretation

The presence of build/test/health/deployment mechanisms means this is substantially more mature than the historical prototypes, but it should be treated as **Core + Harden**, not finished.

## Migration role

This repository becomes the canonical owner for business-side concepts such as:

- User / organization / site
- Content
- Business media asset references
- Workflow
- Publication
- AI capability policy / quota / audit
- Business task submission

It must consume, not own, low-level GPU/media/broadcast runtime details.

## Required next audit

- database schema as canonical source of business objects
- exact API routes and error model
- AI gateway ownership versus Yimeng Intelligence
- artifact/media identity
- auth and organization model
- worker/job state machine
- frontend information architecture
