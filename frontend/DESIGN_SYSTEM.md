# Unified Frontend Design System — Draft 0.1

## Goal

让不同专业应用在用户层面具有同一产品家族的视觉与交互语言，同时允许专业前端技术存在差异。

## Baseline

Production enterprise/desktop web:

- React 19 + TypeScript
- Ant Design 6 as the default enterprise component system
- `@media-digital/ui` as the future ecosystem-level design layer
- Vite for SPA; Next.js only when SSR/app-router is justified
- Playwright + Vitest

Research/demo UIs may use Gradio/Solara, but these are not the production design baseline.

## Design tokens

Canonical tokens must cover:

- color roles, not page-specific colors
- typography scale
- spacing scale
- border radius
- elevation
- motion timing
- status semantics
- light/dark behavior
- localization

Token values should live in one package and be consumed by all production web apps.

## Core interaction vocabulary

The same semantic state should have the same visual treatment across products:

```text
idle
queued
running
paused
succeeded
warning
failed
cancelled
archived
```

Core cross-product components should converge around:

- AppShell
- GlobalSearch
- WorkspaceSwitcher
- TaskStatus
- Progress
- MediaCard
- AssetCard
- ArtifactCard
- AIResult
- EvidencePanel
- SourceList
- MediaPlayer
- Timeline
- EmptyState
- ErrorState
- PermissionDenied

## Product surfaces

### Business surface

For editors, journalists, operators and administrators. Dense data presentation is acceptable, but navigation and state semantics must remain consistent.

### AI Studio

For knowledge workers and AI operators. Must emphasize evidence, model/task status, context and provenance rather than merely chat bubbles.

### Creative Studio

For script/storyboard/timeline workflows. Interaction can be denser and specialized but uses the same shell, token system and task semantics.

### Consumer

WeChat Mini Program may use native components. It must nevertheless follow the same brand vocabulary, content semantics and API/result contracts.

## Prohibited UI patterns

- production application based on Solara/Gradio
- each application inventing a different task status vocabulary
- direct browser access to another application's database
- page-specific API response formats for the same cross-system object
- visually hiding AI-generated provenance where it matters

## Migration strategy

1. Treat current `@news-media/ui` as the first candidate foundation.
2. Identify components that are truly cross-product before extracting them.
3. Publish design tokens and semantic components before attempting a large component-library rewrite.
4. Migrate one representative screen from Business, AI and Creative surfaces to prove the system.
