# Cross-Repository Dependency Rules

## 1. Direction

```text
Experience
   ↓
Business / Application
   ↓
Intelligence / Processing / Live Control
   ↓
Runtime / Engine
   ↓
Infrastructure
```

下层不得反向依赖上层业务代码。

## 2. Allowed dependency forms

Allowed:

- HTTP/REST API
- OpenAPI contract
- Async event contract
- Job submission contract
- Shared schema package containing only stable cross-system types
- S3-compatible artifact access through Artifact identity/locator contract

Discouraged:

- Shared internal implementation package
- Cross-repository ORM model import
- Direct access to another system's database

Forbidden:

- UI imports from another product's private source tree
- Direct SQL against another product's primary database
- Provider-specific assumptions in business capability APIs
- Runtime-specific objects crossing system boundaries

## 3. Data ownership

Every persisted business fact must have exactly one owner.

Consumers may cache, index or materialize read models, but must not create a competing authoritative record without an ADR.

## 4. Database boundary

A repository may connect to its own database/schema. Cross-system integration must use contract APIs/events unless a read replica or analytical export is explicitly defined.

## 5. Storage boundary

Applications consume Artifact identity first. A storage locator may be resolved by a storage service/adapter. URL strings must not become cross-system identity keys.

## 6. Job boundary

Callers submit a semantic Job. They do not manage another system's BullMQ/Celery queue directly.

## 7. AI boundary

Business systems request capabilities. They do not construct provider-specific HTTP payloads or vendor SDK clients.

## 8. Realtime boundary

`VBMF` and `live-platform` expose control semantics. They do not depend on business React components or CMS persistence internals.

## 9. Shared packages

Shared packages should be small and dependency-light:

```text
shared types
contracts
UI primitives
utility primitives
```

Never put domain implementation logic into a global shared package merely to avoid a service boundary.
