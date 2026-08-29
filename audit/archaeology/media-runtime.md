# Archaeology — Media Runtime

## Scope

`live-platform`, `VBMF`, `video-shot-detection`, `video-compression-system`, plus the older `video-management-system` and `city-converged-media-platform` media portions.

## Findings

### Live Platform

A concrete ZLMediaKit-oriented operations console exists with multi-protocol ingest/playback, monitoring, player support, stream URL generation and asset upload. Current implementation uses React 18 + Vite + Ant Design 5 and an Express/Node backend. This is a valid specialized runtime and should continue as Live Operations rather than being absorbed into the content business application.

### VBMF

VBMF is a materially different class of project: a broadcast runtime/fabric with locked runtime semantics, 12 engines, cross-cutting systems/capabilities, health tree, failover/switch modes and a phased implementation roadmap. It must be protected as a specialist broadcast runtime and must not be reduced to generic live-stream CRUD.

### Shot Detection

The project has a coherent single-purpose processing pipeline based on TransNetV2 with visual/motion/blackframe/audio validation, fusion, post-processing and export. It has explicit path traversal protection, subprocess timeouts and structured audit logs. Strong candidate for an engine/service boundary.

### Compression

The project is a focused Python/FFmpeg quality-processing project around re-encoding and VMAF/SSIM/PSNR gating. It is too narrow to justify a general media platform but valuable as a processing engine.

### Video Management System

The older project describes upload, transcode, management, AI analysis and HLS editing, but uses another stack (FastAPI + SQLAlchemy + Vue3 + Element Plus + Celery + Redis) and local/SQLite-to-PostgreSQL assumptions. Its biggest value is historical domain/workflow ideas, not another platform implementation.

### City Converged Media Platform

An earlier broad architecture combining SRS, FFmpeg, ONNX Runtime, Vue3, FastAPI and SQLite/PostgreSQL is documented as a government-oriented converged platform. It duplicates functions now better separated into content, live, AI and runtime planes.

## Target boundaries

```text
Business Platform
   ↓ API / Command / Event
Live Operations ──────────────── Broadcast Runtime
   │                                 │
ZLMediaKit                         VBMF

Business/AI processing jobs
   ↓
Media Processing Engines
   ├── Shot Detection
   ├── Compression / Quality
   ├── ASR
   ├── OCR
   └── Transcode
```

## Rules

- `live-platform` owns live operational concepts, not articles or global content metadata.
- `VBMF` owns broadcast/runtime semantics, not user-facing CMS workflows.
- Processing engines are stateless or job-oriented where possible and communicate through Artifact/Job contracts.
- `video-management-system` and `city-converged-media-platform` must not be revived as competing platform cores.

## Migration

Extract proven algorithms and operational patterns. Rebuild the integration/API surface against the new canonical contracts. Avoid direct database sharing between business and runtime projects.
