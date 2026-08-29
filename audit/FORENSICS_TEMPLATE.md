# Repository Forensics Template

> 用于每一个被审计仓库。所有结论必须区分“事实”“推断”“待验证”。

## 1. Repository Identity

- Repository:
- Default branch:
- Visibility:
- Last meaningful commit:
- Current disposition:
- Target role:

## 2. Evidence

| Area | Evidence | Level | Confidence | Notes |
|---|---|---:|---|---|
| README | | E0 | | |
| Source | | E1 | | |
| Executable path | | E2 | | |
| API+persistence+runtime | | E3 | | |
| Real environment | | E4 | | |

## 3. Functional Archaeology

### Claimed

### Implemented

### Integrated

### Verified

### Production

## 4. Functional Closure

For every major feature:

```text
UX entry
→ command/API
→ validation
→ persistence/state
→ async/runtime
→ artifact/result
→ error/retry/recovery
→ test
→ real verification
```

Record the first broken edge.

## 5. Domain Model

List all major objects and identify:

- canonical candidate
- local projection
- duplicate
- ambiguous meaning
- obsolete object

## 6. API

Record:

- route
- method
- auth
- request schema
- response schema
- idempotency
- pagination
- error model
- async semantics
- versioning

## 7. Jobs / Workers

Record:

- Task vs Job semantics
- queue/runtime
- state machine
- retry
- timeout
- cancellation
- orphan recovery
- idempotency
- output artifact

## 8. Storage

Record:

- DB
- object storage
- cache
- file paths
- artifact identity
- checksum
- retention
- provenance

## 9. Frontend

Record:

- routes
- information architecture
- design system
- state model
- loading/error/empty states
- accessibility
- responsive behavior
- API coupling
- duplicated UI

## 10. Security / Operations

Record:

- authentication
- authorization
- secret handling
- SSRF/path traversal/resource exhaustion
- audit
- logs
- metrics
- tracing
- health/readiness
- deployment

## 11. Reusable Assets

Classify each item:

- domain rule
- schema
- API contract
- algorithm
- engine
- UI pattern
- test
- migration
- documentation
- historical debt

## 12. Final Decision

- KEEP
- HARDEN
- CONSOLIDATE
- REBUILD
- EXTRACT
- FREEZE
- RETIRE

## 13. Migration Actions

| Asset | From | Destination | Action | Priority | Verification |
|---|---|---|---|---|---|
| | | | | | |

## 14. Open Questions

Anything that could change the disposition must be listed explicitly.
