# Repository Architecture Manifest Standard

每个生态仓库最终应提供 `architecture-manifest.yaml`。这是跨仓库治理的机器可读入口，用于 AI coding agent、CI 与人工审核判断项目当前真实角色。

## Minimal schema

```yaml
schema_version: 1
system_id: example
repository: owner/example
role: platform # platform|engine|runtime|studio|application|lab|legacy
lifecycle: active # active|consolidating|frozen|legacy|retired
health: yellow # green|yellow|orange|red
last_verified_commit: ""
owned_domains: []
provided_capabilities: []
consumed_contracts: []
owned_objects: []
forbidden_dependencies: []
runtime:
  language: ""
  framework: ""
data:
  primary_store: ""
  object_storage: ""
execution:
  queue: ""
  realtime: false
observability:
  tracing: opentelemetry
```

## Rules

- `role` describes what the repository is supposed to be, not what its README hopes to become.
- `health` describes actual completion and operational confidence.
- `last_verified_commit` must be updated after architecture audit.
- `owned_objects` must contain only canonical ownership; derived/read-only views go elsewhere.
- `forbidden_dependencies` must describe prohibited reverse dependencies.

## Health interpretation

`green` = complete enough for current declared role.

`yellow` = usable but with bounded gaps.

`orange` = partial closure; must not become a new source of truth.

`red` = abandoned/experimental/broken/mostly mocked; migration or retirement decision required.

## Required CI checks (future)

- Manifest parses.
- Role is known.
- No duplicate canonical owner for the same domain/capability.
- Contract versions are valid.
- Forbidden dependency rules are not violated.
- Last verified commit is present for production repositories.
