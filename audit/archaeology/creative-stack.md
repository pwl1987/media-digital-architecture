# Archaeology — Creative Platform Stack

## Scope

`media-ai-platform`, `lamice`, `lamice-platform` are treated as multiple generations of one Creative domain, not three independent products.

## Evidence

### `media-ai-platform`

Repository documentation/code evidence indicates a Next.js + React 19 + Prisma + MySQL + Redis/BullMQ based creative runtime with workers, watchdog/reconciliation concepts, provider/capability controls and billing-related infrastructure.

### `lamice`

The repository describes a Next.js 15 + React 19 + Prisma + MySQL + Redis + BullMQ application covering script analysis, character/scene generation, storyboard/video production and voiceover. It explicitly calls CapCut export and compliance checking experimental and non-MVP.

### `lamice-platform`

The later platform branch moves to FastAPI + SQLAlchemy + Redis + APScheduler and Vue3 + Element Plus, with pluginized `module_lamice`, workflow/billing/provider services, SSE and tests. Its own status table documents that editor functionality remains skeleton, storage routing is incomplete, project/episode status is missing, prompt management is absent, and several slices remain open.

## Archaeological conclusion

These are not three platforms worth independently completing. They represent three architectural attempts around the same business domain. The expensive mistake would be to preserve all three runtimes and reconcile them later.

## Target

```text
Creative Platform Core
        ↑
   LAMICE Studio
```

The core owns:

- CreativeProject
- Episode / Story structure
- Character / Location / Asset references
- StoryboardShot / StoryboardPanel
- TimelineClip
- Generation requests/results
- Creative workflow
- Rendering/export orchestration

The Studio owns user experience and editing workflows; it must not create a second identity, asset, job or provider universe.

## Keep / Extract / Rebuild

### Keep

- storyboard and creative object ideas
- generation workflow concepts
- provider abstraction where it is domain-appropriate
- billing/accounting ideas only after redesign around platform-wide identity and usage contracts
- useful worker patterns

### Extract

- reusable media-generation adapters
- outbox/reconciliation ideas
- workflow state transitions
- render/timeline concepts

### Rebuild

- canonical creative schema
- storage/artifact references
- task/job/generation model
- auth integration
- API contracts
- UI information architecture

### Retire

- duplicate database ownership
- duplicate global provider settings
- duplicate user/auth systems
- ad-hoc URL fields as asset identity
- duplicate task engines with incompatible semantics

## Hard decision

Do not start a fourth Creative repository until the canonical Creative domain model and contracts in `media-digital-architecture` are approved.
