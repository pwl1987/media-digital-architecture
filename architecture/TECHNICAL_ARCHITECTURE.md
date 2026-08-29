# Technical Architecture — Draft 0.2

## 1. 目标

技术架构只负责保证多个专业系统能够形成一个稳定生态，不以“所有项目必须同栈”为目标。

当前已验证的主要技术事实：

| 系统 | 主要技术事实 | 架构判断 |
|---|---|---|
| `news-media-system` | Fastify 5 + PostgreSQL + Drizzle + BullMQ/Redis-compatible + React 19/Vite + Ant Design 6 + shared/ui packages | Business Control Plane 基础较成熟 |
| `YimengSpirit-Multimodal` | Python 3.12 + Transformers/PyTorch + YAML/env configuration；生产 extra 仍在建设 | Intelligence Runtime / AI domain |
| `media-ai-platform` | Next.js 15 + React 19 + Prisma/MySQL + Redis/BullMQ + Remotion + 多 provider SDK | 与 LAMICE 高度重叠 |
| `LAMICE` | Next.js + React 19 + Prisma/MySQL + Redis/BullMQ；独立 worker/outbox/watchdog | 应收敛为 Creative Studio + Creative Platform |
| `live-platform` | React 18 + Vite + AntD 5；独立 server/client；ZLMediaKit/FFmpeg 运行时 | Live Operations |
| `VBMF` | Rust/GStreamer/FFmpeg/DeckLink 等广播运行时语义 | Realtime Broadcast Fabric |

## 2. 技术统一层级

### 必须统一

- Resource identity
- API semantics
- Error model
- Job lifecycle semantics
- Event semantics
- Artifact provenance
- Authentication propagation rules
- Observability fields
- Versioning
- Design language

### 不要求统一

- 编程语言
- 数据库实现
- Queue 实现
- Web framework
- 部署形态
- 模型 runtime

## 3. Service boundary

```text
Business API
    ↓
Intelligence / Processing / Live API
    ↓
Specialized Runtime
    ↓
Infrastructure
```

系统之间只依赖公开 Contract，不直接访问其他系统数据库或内部模块。

## 4. AI architecture

`news-media-system` 已有 AI Gateway / capability / provider / route / quota / audit 体系；这些属于 Business AI Control Plane。其公共类型当前已经覆盖 `llm/vlm/asr/tts/embedding/ocr/image/video` 等能力。fileciteturn136file0L2-L2

Yimeng Intelligence 不应重复拥有业务级 provider registry；它应提供模型执行、RAG、知识、证据和评估等 Intelligence/Data Plane 能力。

建议关系：

```text
Capability
  ↓
Policy / Routing
  ↓
Provider / Model
  ↓
Runtime
  ↓
Artifact / Result
```

## 5. Frontend architecture

`news-media-system` 已经存在 React 19 + Ant Design 6，并有 `@news-media/shared` 与 `@news-media/ui` 源码共享包。fileciteturn130file0L2-L2 fileciteturn140file0L2-L2

这应作为企业 Web UI 的参考基线。

`live-platform` 仍为 React 18 + AntD 5；不要求立即重写，但新跨平台公共组件不应再复制第二套设计语义。fileciteturn117file0L2-L2

Solara/Gradio 等保留给 Research/Engine UI，不升级为企业主产品 UI。

## 6. Creative platform convergence

`media-ai-platform` 当前 package scripts 已包含 Next server、worker、watchdog、Bull Board，以及大量 provider/capability/task/coverage guards。fileciteturn134file0L2-L2

`LAMICE` 也运行独立的 Next server、BullMQ workers、outbox dispatcher、watchdog/log cleanup。fileciteturn131file0L2-L2 fileciteturn132file0L2-L2

结论：两套 Creative runtime 不应继续并行定义同一类业务状态。目标应是：

```text
Creative Platform
  ├── project / episode / character / location
  ├── generation / task / artifact
  ├── provider/model orchestration
  ├── timeline/render
  └── usage/audit
          ↑
     LAMICE Studio
```

## 7. Configuration

当前生态存在数据库配置、ENV、YAML、自定义 resolver 等多套方式。不要强行统一文件格式；必须统一最终解析语义：

```text
Source
  ↓
Resolver
  ↓
Typed Runtime Config
  ↓
Startup Validation
```

禁止业务代码在多个位置自行猜 provider/model/default。

## 8. Storage

业务数据库保存 metadata/identity；对象存储保存 bytes；Artifact Registry 保存二者关系与 provenance。

```text
Artifact ID
    ├── metadata
    ├── storage locator(s)
    ├── checksum
    ├── producer/version
    └── lineage
```

## 9. Runtime isolation

- 广播 realtime runtime 不接受 Web UI 逻辑依赖。
- AI model runtime 不接受 CMS 数据库直接依赖。
- Processing Engine 不知道具体消费者是谁。
- Consumer MiniApp 不直接访问数据库。
- Research Lab 不成为 production runtime 的源码依赖。

## 10. Observability baseline

跨系统至少共享：

```text
trace_id
request_id
job_id
artifact_id
actor_id
organization_id
producer
producer_version
status
error_code
latency_ms
```

这套字段最终应进入统一日志/trace/event 约定。

## 11. 下一步

本文件仍是 Draft。正式 V1.0 前必须继续核对：

1. 每个仓库实际 API route/DTO。
2. 每个数据库 schema 的字段冲突。
3. 所有 Job state machine。
4. 所有 object-storage reference。
5. Auth token propagation。
6. Event publishing/consuming。
7. Frontend route/component ownership。
8. Docker/network topology。
