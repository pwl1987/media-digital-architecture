# Platform Boundaries V1

## 目标

避免同一领域被多个项目重复实现。统一的是 ownership 和 contract，而不是仓库数量。

## Canonical Platform Ownership

| Domain | Canonical owner | Supporting systems |
|---|---|---|
| Identity / Organization | Media Digital Platform | All applications |
| Content / Article / CMS | news-media-system | Consumer / AI / Creative |
| Media Asset business metadata | news-media-system | Processing Engines |
| AI governance / business capability | news-media-system | Yimeng Intelligence |
| AI inference / RAG / knowledge | Yimeng Intelligence | All consumers |
| Media processing | Media Processing Engines | News / AI / Creative |
| Live operations | live-platform | News / Portal |
| Broadcast runtime | VBMF | Live / News / Operations |
| Creative production domain | Creative Platform | LAMICE Studio |
| Dataset annotation | Data Studio | Yimeng Intelligence / Research |
| Model research | Yimeng Research Lab | Yimeng Intelligence |
| Consumer cultural experience | Yimeng Culture App | All services |

## Ownership Rules

1. A canonical object has exactly one system of record.
2. A capability may have many implementations during migration, but only one production owner.
3. Consumers may cache or materialize derived views but may not silently become a second source of truth.
4. Direct database access across bounded contexts is forbidden unless an ADR explicitly permits it.
5. Cross-boundary integration uses versioned API/event contracts.
6. A new platform must prove why an existing owner cannot provide the capability before creating a new owner.

## Data Flow

```text
Experience
   ↓
Business Control
   ↓
Intelligence / Processing
   ↓
Runtime
   ↓
Infrastructure
```

## Non-Goals

- Do not merge VBMF into a CMS.
- Do not turn Yimeng Intelligence into another CMS.
- Do not turn media engines into user-facing business platforms.
- Do not make the consumer miniapp own enterprise content truth.
- Do not make research repositories production dependencies.
