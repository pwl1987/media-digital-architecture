# Repository Architecture Matrix — Draft 0.1

> This matrix captures the current architectural role of the ecosystem. It is intentionally conservative; implementation facts will continue to be verified against source code.

| Repository | Primary role | Owns business truth? | Owns runtime? | Primary UI? | Target fate |
|---|---|---:|---:|---:|---|
| `news-media-system` | Content / Business Platform | Yes | Partial | Yes | Core |
| `YimengSpirit-Multimodal` | Intelligence / Knowledge | Intelligence truth | AI runtime | Internal/AI Studio | Core |
| `VBMF` | Broadcast Fabric | Broadcast runtime truth | Yes | Ops/internal | Core |
| `live-platform` | Live Operations | Live operational truth | Yes | Yes | Core |
| `video-shot-detection` | Processing Engine | No | Engine | No | Engine |
| `video-compression-system` | Processing / Quality Engine | No | Engine | No | Engine |
| `media-ai-platform` | Creative Production Platform | Creative truth | Worker/orchestration | Yes/internal | Consolidate |
| `LAMICE` | Creative Studio | No | No | Yes | Consolidate |
| `ai-spider-annotation` | Data Studio | Dataset working truth | Data jobs | Yes | Supporting |
| `yimengjingshen` | Research Lab | Research artifacts | Training runtime | Experiment UI | Research |
| `xiao-opera-miniapp` | Consumer Experience | No | No | Yes | Application |
| `media-platform` | Legacy Media Platform | Historical | Historical | Historical | Freeze/retire |
| `YimengHeart` | Legacy AI Chat | Historical | Historical | Historical | Compatibility/retire |
| `media-digital-platform` | Unified Experience Shell (proposed) | No | No | Yes | New theme platform |

## Canonical ownership proposal

| Capability / object | Canonical owner |
|---|---|
| User / Organization / Site | `news-media-system` or dedicated identity service in future |
| Content | `news-media-system` |
| Business Media Asset registration | `news-media-system` |
| Artifact registry semantics | Shared contract; ownership to be finalized during Schema Audit |
| Live Stream / Channel | `live-platform` |
| Broadcast Source / Fabric / Switch State | `VBMF` |
| Video Shot analysis | `video-shot-detection` |
| Compression / Quality Report | `video-compression-system` |
| Knowledge / Evidence | Yimeng Intelligence |
| Dataset / Annotation | Data Studio + Research workflow |
| Model Artifact | Model/Research lifecycle; production registry TBD |
| CreativeProject / Generation | `media-ai-platform` after consolidation |
| Creative UX | `LAMICE` |

## Current technical baseline evidence

`news-media-system` has a production-oriented Node/Fastify/PostgreSQL/Drizzle/BullMQ stack, React 19/Vite/Ant Design 6 frontend, and shared `@news-media/shared` / `@news-media/ui` packages.

`YimengSpirit-Multimodal` is Python 3.12 oriented with PyTorch/Transformers and a separate AI serving architecture.

`media-ai-platform` and `LAMICE` both use Next.js/React 19, Prisma/MySQL and BullMQ-style worker infrastructure, which confirms high consolidation pressure.

These statements are baseline observations, not a final compatibility certification.

## Next evidence to collect

- full Prisma/Drizzle/SQLAlchemy model comparison
- REST route inventory
- request/response schema inventory
- auth/session/tenant implementation
- queue names and state transitions
- storage bucket/path conventions
- asset/media/artifact IDs
- provider/model registries
- frontend route and navigation inventory
