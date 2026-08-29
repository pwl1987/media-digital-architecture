# Technology Fact Matrix — 2026-08-29 / Draft 0.2

> 本表只登记已经通过当前仓库源码/配置文件看到的事实；“目标角色”属于架构判断。后续继续补全，不能把未检查路径视为已验证。

| Repository | Verified facts | Current risk | Target role |
|---|---|---|---|
| `news-media-system` | Backend: Fastify 5, Drizzle, PostgreSQL, BullMQ, Redis-compatible, S3 SDK, FFmpeg；Frontend: React 19, Vite, Ant Design 6, React Router 7；存在 `@news-media/shared`、`@news-media/ui`。fileciteturn129file0L2-L2 fileciteturn130file0L2-L2 fileciteturn135file0L2-L2 fileciteturn140file0L2-L2 | 中：已有较成熟 AI/control 体系，但跨系统边界仍需核对 | Business Control Plane / Content System of Record |
| `YimengSpirit-Multimodal` | Python 3.12；MiniCPM-V 4.6；PyTorch/Transformers 推理；YAML/env；production extra 仍预留 vLLM/FastAPI/FAISS；`inference.py` 当前明确覆盖文本、单图和当轮单图多轮路径。fileciteturn142file0L2-L2 fileciteturn138file0L2-L2 | 高：产品定位超过实际已落地 runtime；需继续拆 Intelligence / Data / Serving | Yimeng Intelligence Plane |
| `media-ai-platform` | Next.js/React 19；Prisma/MySQL；Redis/BullMQ；Remotion；多 AI SDK；大量 provider/capability/task/billing/architecture guard；独立 worker/watchdog/Bull Board。fileciteturn134file0L2-L2 | 高：与 LAMICE 高度重叠 | Creative Production Platform |
| `lamice` | Next.js/React 19；Prisma/MySQL；独立 BullMQ image/video/music/voice/text workers、outbox worker/dispatcher；丰富 Creative schema。fileciteturn131file0L2-L2 fileciteturn132file0L2-L2 fileciteturn139file0L2-L2 | 高：第二套 Creative runtime/Project/Media/Task 世界 | Creative Studio + converged platform |
| `live-platform` | Web client: React 18 + Vite + AntD 5 + hls.js/flv.js；独立 server/client；ZLMediaKit/FFmpeg 目录与部署资产。fileciteturn117file0L2-L2 fileciteturn114file0L2-L2 | 中：与 news-media 有直播交集，但抽象层不同 | Live Operations Platform |
| `VBMF` | Rust/GStreamer/FFmpeg/DeckLink 相关运行时；服务、ops、evidence、scripts 独立；已有广播级架构基线。fileciteturn115file0L2-L2 | 低/边界风险：不能被普通 Web 平台侵入 | Broadcast Realtime Fabric |
| `yimengjingshen` | MiniMind/研究训练路线，包含 transformers/trl/datasets/swanlab/model tooling。 | 高（若直接生产化）：研究代码与产品运行时耦合 | Model Research Lab |
| `ai-spider-annotation` | 已确认定位为采集、数据管理、标注、AI 辅助和导出工具；当前独立 Vue/FastAPI/SQLite 路线。 | 中高：数据源与知识资产未统一 | Data Studio |
| `video-shot-detection` | 专业镜头检测 pipeline，包含视觉/运动/黑场/音频/融合/NMS/关键帧等能力。 | 中：需要标准 Job/Artifact 输出 | Shot Detection Engine |
| `video-compression-system` | FFmpeg 重编码 + VMAF/SSIM/PSNR 等质量门禁。 | 中：需要进入统一 Media Processing contract | Compression / Quality Engine |
| `media-platform` | 旧一代融媒体后端，FastAPI/PostgreSQL/SQLAlchemy/Celery/Redis/MinIO 路线。 | 高：第二套业务平台 | Legacy / Migration Source |
| `YimengHeart` | Flask + DashScope 的历史单一问答入口。 | 高：历史产品边界 | Legacy Compatibility |
| `xiao-opera-miniapp` | 消费侧小程序；当前 AI 创作层仍有 mock/simulation 路径。 | 中高：体验端与真实 Intelligence API 尚未完全闭环 | Consumer Experience |

## 2. 已确认的关键技术冲突

### React / UI

- `news-media-system`: React 19 + AntD 6。fileciteturn130file0L2-L2
- `live-platform`: React 18 + AntD 5。fileciteturn117file0L2-L2
- `media-ai-platform` / `LAMICE`: Next.js + React 19 + Tailwind。fileciteturn134file0L2-L2 fileciteturn133file0L2-L2

结论：不强行统一框架，但应统一 Design System、领域对象和 API Contract。

### Database

目前已确认至少存在 PostgreSQL、MySQL、SQLite 三个数据世界；这不是立即迁成一个数据库的理由，但必须禁止跨系统直接读库。

### Queue

已确认 BullMQ 在多个 Node 平台出现，而 legacy media platform 使用 Celery；VBMF 使用专用 realtime runtime。结论是统一 Job Contract，不统一 Queue 实现。

### AI Provider

`news-media-system` 已有 AI provider/capability 类型，覆盖 `llm/vlm/asr/tts/embedding/ocr/image/video`，并存在 `AIAdapter` 抽象。fileciteturn136file0L2-L2 fileciteturn137file0L2-L2

这应属于业务侧 AI Control Plane；生产 Intelligence 应暴露稳定能力接口，而不是复制另一套业务 provider registry。

## 3. 直接暴露出的架构动作

1. 冻结继续扩张的第二套 CMS / Media Platform。
2. `media-ai-platform` 与 `LAMICE` 停止重复定义 Creative 核心对象。
3. 统一 Asset/Artifact/Job/Evidence/Generation 的跨系统语义。
4. 将 Shot Detection / Compression 视为标准 Engine。
5. 将 Live 与 Broadcast 保持不同 runtime 边界。
6. 建立跨系统 identity / trace / job / artifact provenance。

## 4. 本表下一轮必须补齐

- 完整 DB table/model inventory
- API route + DTO inventory
- Auth/session/JWT propagation
- Storage bucket/key/URI 规则
- Worker queue/task type inventory
- Event producer/consumer inventory
- Frontend route + page ownership
- Docker/network/service topology
- CI gate matrix
