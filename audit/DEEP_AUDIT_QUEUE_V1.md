# Deep Audit Queue V1

## Audit order

### Wave 1 — Core Product and AI

1. `news-media-system`
2. `YimengSpirit-Multimodal`
3. `media-ai-platform`
4. `lamice`
5. `lamice-platform`

Goal: determine the target business, intelligence and creative cores.

### Wave 2 — Media Runtime

6. `live-platform`
7. `VBMF`
8. `video-shot-detection`
9. `video-compression-system`

Goal: define realtime/media-processing boundaries and reusable engines.

### Wave 3 — Data, Research and Consumer

10. `ai-spider-annotation`
11. `yimengjingshen`
12. `xiao-opera-miniapp`
13. `YimengHeart`

Goal: preserve data, research and experience assets while removing duplicate runtime ownership.

### Wave 4 — Historical/Peripheral Portfolio

14. `media-platform`
15. `city-converged-media-platform`
16. `video-management-system`
17. other discovered media/AI prototypes

Goal: extract only proven assets and close historical debt.

## Per-repository audit depth

### D1 — Structure

Tree, languages, package managers, entry points, build/run paths.

### D2 — Domain

Schema, objects, ownership, state machines and persistence.

### D3 — API

Routes, DTOs, auth, errors, idempotency, sync/async semantics and versioning.

### D4 — Runtime

Workers, queues, external providers, storage, retries, cancellation, recovery and resource limits.

### D5 — Frontend

Routes, UX flows, states, design system, API coupling and accessibility.

### D6 — Verification

Tests, CI, runtime smoke, real environment, operational evidence.

### D7 — Disposition

KEEP / HARDEN / CONSOLIDATE / REBUILD / EXTRACT / FREEZE / RETIRE.

## Promotion rule

No historical module is promoted into a target platform merely because it exists or appears feature-rich.

Promotion requires:

```text
Evidence
+ domain ownership
+ contract compatibility
+ test evidence
+ operational fit
+ migration plan
```

## Exit criteria for Wave 1

Before implementation begins on the unified theme platform, Wave 1 must establish:

- canonical business objects
- canonical creative objects
- AIResult and Evidence model
- Asset/Artifact identity
- Task/Job semantics
- shared error model
- identity/permission boundary
- storage ownership
- front-end design system boundary
- creative-platform consolidation decision

## Status

- Wave 1: IN PROGRESS
- Wave 2: QUEUED
- Wave 3: QUEUED
- Wave 4: QUEUED
