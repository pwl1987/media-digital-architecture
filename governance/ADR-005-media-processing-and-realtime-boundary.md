# ADR-005 — Media Processing and Realtime Boundaries

- Status: PROPOSED
- Date: 2026-08-29

## Decision

媒体生态分成三个运行时域：

1. **Media Processing** — 非实时、可排队、可重试的计算。
2. **Live Operations** — 流媒体会话与运营控制。
3. **Broadcast Runtime** — 帧/时钟/冗余/切换敏感的广播级实时运行时。

### Media Processing

代表：

- `video-shot-detection`
- `video-compression-system`
- future ASR / OCR / subtitle / thumbnail / transcode engines

统一输入输出：

```text
input Artifact
  ↓
Job
  ↓
Engine
  ↓
output Artifact(s)
  ↓
Event
```

Engine 不拥有业务项目、业务用户或发布工作流。

### Live Operations

代表：`live-platform`。

负责：

- stream/session/channel
- ingest/playback
- streaming state
- operational monitoring
- user-facing live configuration

### Broadcast Runtime

代表：`VBMF`。

负责：

- broadcast source/fabric
- realtime health
- redundancy
- switching
- frame-accurate or timing-sensitive processing
- hardware/media runtime

不应被普通 HTTP CRUD 或通用业务 Job 模型侵入。

## Integration boundary

```text
Business / Operations
        ↓
Control API
        ↓
Live / Broadcast Runtime
```

上层不能直接操作：

- DeckLink SDK
- GStreamer internals
- FFmpeg process details
- ZLMediaKit internals

除非该系统本身就是对应 Engine/Runtime。

## Consequences

- 处理引擎可以独立扩容和 GPU 化。
- 实时运行时可以独立保证时序和故障切换。
- 业务平台只依赖稳定控制契约。
- 同一个媒体资产可以同时产生实时与离线派生产物，而不混淆生命周期。
