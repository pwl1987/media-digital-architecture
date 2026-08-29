# Archaeology — live-platform

## 定位

`live-platform` 应保留为 **Live Operations Platform**，不与 `VBMF` 或 `news-media-system` 直接合并。

README 明确其核心是 ZLMediaKit 直播运营中台，覆盖 RTMP/RTSP/HLS/HTTP-FLV/WebRTC/SRT、房间、拉源、播放器、资源监控、告警与素材库。fileciteturn169file0L2-L2

## 已确认资产

- ZLMediaKit runtime integration。
- React 18 + Vite + TypeScript + Ant Design 5 控制台。
- Node.js 24 + Express server。
- FFmpeg-as-a-Service 镜像。
- GHCR 镜像发布体系。
- Docker Compose 部署。
- CI 包括 backend test、frontend build。
- 密码、2FA、审计日志、登录限流等安全设计。fileciteturn169file0L2-L2

## 主要问题

### 1. 前端基线落后于生态

React18/AntD5 与未来 React19/AntD6 不一致；不需要立即重写，但所有新增跨系统公共 UI 不应复制这套版本依赖。

### 2. Express 与业务主平台 Fastify 不一致

直播平台继续保持独立可以接受；如果未来扩大为通用业务后台，应避免从 Live Domain 向 Business Platform 反向扩张。

### 3. 默认密码虽然有 fail-safe 规则，但仍然反映出产品 onboarding 设计不够成熟

README 仍以 `admin123` 首次登录为说明并要求用户修改；长期应改成一次性 bootstrap credential 或初始化向导，而不是固定默认密码。fileciteturn169file0L2-L2

### 4. Live 与 Broadcast 的边界必须继续保持

ZLMediaKit streaming operations 和 VBMF 的 SDI/IP broadcast fabric 不是同一个运行域；上层可以统一 `LiveSession`/`BroadcastSession` 的控制语义，但不能共享内部实现。

## 可复用资产

- Live stream lifecycle
- ZLM control integration
- protocol/player support
- monitoring/alert patterns
- streaming container topology
- GHCR release pipeline

## 不建议迁移

- 直接把 ZLM internal APIs 提升为企业通用内容 API。
- 把直播房间模型强行作为全局 `Project`。
- 把 Live runtime 与 VBMF runtime 代码合并。

## 最终命运

**Recover + Align**

保持独立运行，逐步接入统一：

- Identity
- Session contract
- Job/Event semantics
- Asset/Artifact
- Observability
- Design system

## 后续尸检重点

1. 实际 stream/session DB schema。
2. API routes 与认证传播。
3. ZLM callback 生命周期。
4. 录制 → Asset → Content 的闭环。
5. 故障恢复/重连/断流状态机。
6. 前端核心页面实际完成度。
