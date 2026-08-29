# Archaeology — news-media-system

## 定位

当前生态最合适的 **Business Control Plane / Content System of Record** 候选。README 明确为前后端分离 monorepo：backend Fastify + PostgreSQL + Drizzle，frontend React 19 + Vite + Ant Design Pro；并包含媒体队列、worker、Docker、MinIO/对象存储与 AI 能力。fileciteturn167file0L2-L2

## 已确认的强项

- 技术基线最接近未来 Business Platform 标准：Fastify/PostgreSQL/Drizzle/BullMQ/React19/Vite/AntD6。
- 已有 `@news-media/shared` 与 `@news-media/ui`，说明已经存在跨前端共享契约/组件沉淀。
- AI Gateway 已存在 capability/provider/adapter 体系，公共 capability 覆盖 llm/vlm/asr/tts/embedding/ocr/image/video。fileciteturn136file0L2-L2
- AI adapter 有独立接口，避免业务代码直接绑定厂商。fileciteturn137file0L2-L2
- README 对轻量/标准部署、worker 隔离、失败重试、dead-letter、降级、密钥等已经有明确说明。fileciteturn167file0L2-L2

## 当前主要问题

### 1. “业务主系统”和“AI 平台”边界仍在形成

AI Gateway 已足够强，继续向 Yimeng AI 中增加同类 provider registry / quota / audit 会造成双 Control Plane。当前母架构已将这类职责归为 Business AI Control Plane，而 Yimeng Intelligence 归为 Data/Execution Plane。

### 2. 部署语义存在双模式复杂度

轻量档 backend 可以同时跑 `media,trim,ai,scheduler`，标准档则把 ai/trim 拆到独立 worker；README 特别警告忘记修改 `BACKEND_WORKER_ROLES` 会造成双跑。fileciteturn167file0L2-L2

结论：短期可保留，长期应把“业务进程角色”和“部署 profile”解耦成显式 Runtime Contract，而不是依赖环境变量组合。

### 3. 共享 package 的边界不能继续模糊扩大

`@news-media/shared` 很有价值，但不应成为所有系统的全局领域事实源。跨系统对象/事件必须进入母架构版本化 contracts。

### 4. 本地开发和生产语义不能只靠 README 记忆

“Redis 不存在会导致 pending”“不同档位双跑风险”等都属于启动前可机器检查的事实。未来应变成 startup validation / CI guard，而不是文档警告。

## 高价值可复用资产

- Business backend baseline
- React/AntD enterprise UI baseline
- Shared/UI package 组织方式
- AI capability registry + adapter contract
- Media worker / scheduler / dead-letter 经验
- Docker / S3 / PostgreSQL 运维基线

## 不建议继续扩张的方向

- 第二套知识库产品
- 第二套 AI provider governance
- 第二套 creative project system
- 第二套底层媒体 runtime

## 目标命运

**Recover + Core**

不是重建。核心业务资产应该继续保留，后续重点是：

1. 收紧 Business/Intelligence/Processing 边界。
2. 把跨系统 Contract 外移。
3. 把 Asset/Artifact/Job/Event 逐步对齐母架构。
4. 统一主题 Shell/Design System 接入。
5. 将现有“文档警告”逐渐变成机器可验证 guard。

## 当前证据等级

- Runtime/代码：高
- Schema：待全面核对
- API：中高，需全 route/DTO inventory
- UI：中，需要逐页体验审计
- 生产完成度：不可仅根据 README 判定
