# Portfolio Archaeology — 2026-08-29

本报告把当前媒体/AI 相关仓库按“考古”而不是“维护”方式审查。核心原则：README 的功能清单只是声明；只有代码、Schema、测试、CI、可运行入口和真实数据才能作为完成度证据。

## 1. 判定方法

每个仓库从 10 个方面判断：

- 产品闭环：入口 → 核心动作 → 持久化 → 异步/运行时 → 结果 → 失败恢复。
- 功能真实度：真实实现、局部实现、Mock、骨架/占位。
- 运行完整度：开发、测试、生产部署是否能够自洽。
- 数据完整度：核心业务数据是否真实闭环。
- 工程质量：类型、测试、迁移、CI、日志、可观测性。
- 架构适配：是否适合目标母架构。
- 重复度：是否与其他仓库争夺同一职责。
- 可迁移资产：Schema、算法、UI、协议、测试、文档、经验。
- 维护成本：依赖老化、多套技术栈、历史兼容等。
- 最终命运：Recover / Rebuild / Extract / Freeze / Retire。

## 2. 当前证据摘要

| Repository | 证据 | 初步判断 | 建议 |
|---|---|---|---|
| `news-media-system` | Fastify/PostgreSQL/Drizzle/BullMQ + React19/Vite/AntD6；已有 AI gateway/shared/ui；Docker/worker 有较完整说明 | 当前最接近业务主系统，但仍存在本地/标准档双语义和 AI provider 边界问题 | Recover + Core |
| `YimengSpirit-Multimodal` | Python3.12；MiniCPM-V；当前推理核心覆盖文本、单图、多轮；生产 extra 尚在建设 | AI 骨架真实但产品闭环未完成；属于重建型核心 | Rebuild/Continue |
| `media-ai-platform` | Next15/React19/Prisma/MySQL/Redis/BullMQ/Remotion；大量 guard、worker、watchdog、billing/task checks | 工程投入很大，但与 LAMICE 严重争域 | Consolidate |
| `lamice` | Next15/React19/Prisma/MySQL/BullMQ；README 明确标出 CapCut/合规为实验性；主创作链存在 | 真实产品方向明确，但运行职责与 media-ai-platform 重复 | Consolidate |
| `lamice-platform` | FastAPI + SQLAlchemy/Alembic + Vue3/ElementPlus；312 tests/91% coverage 声明；同时 README 自承 Storage、状态字段、编辑器等关键缺口 | 高质量但明显未完成；实际上是另一代 LAMICE 后端平台候选 | Rebuild/Selectively merge |
| `live-platform` | ZLMediaKit + React18/AntD5 + Express；有镜像、CI、协议/播放器/资源监控；默认密码/运维细节仍明显 | 直播控制面可保留，但前端/业务技术线偏旧 | Recover + align |
| `VBMF` | V0.2/Phase0.5 有大量明确语义、对象、surface、fault injection 计划；Runtime Semantics CLOSED | 不是烂尾项目；核心问题是实现阶段尚未跟上规范阶段 | Protect + implement |
| `video-shot-detection` | V4 pipeline 已明确由 TransNetV2 + visual/motion/black/audio + fusion/NMS/postprocess 组成；有安全/审计/CLI | 能力引擎价值高，产品化外壳不应继续扩张 | Extract |
| `video-compression-system` | Python，FFmpeg + VMAF/SSIM/PSNR；仓库仅约 1.2MB，含 main/cli/app/docs/plans/tests；无公开 README 可作为完成证据 | 明显是能力 PoC/工程骨架，不能按“完整系统”评估 | Extract / Freeze |
| `ai-spider-annotation` | FastAPI + Scrapy + SQLite + Vue3/ElementPlus；README 的开发计划仍有模型、爬虫、标注、导出、测试等大量未完成项 | 典型半成品；直接并入新 Data Studio 更合理 | Rebuild |
| `yimengjingshen` | MiniMind 全训练链路研究项目；定位天然是 research/tutorial | 有很高技术资产，但不应成为生产平台 | Lab |
| `xiao-opera-miniapp` | 微信原生；README 宣称完整用户/视听/AI/活动能力，但实际 AI 曾采用模拟生成路径 | 产品壳有价值，后端/AI 需重建 | Rebuild as Consumer |
| `YimengHeart` | Flask + DashScope 的早期问答形态 | 历史产品，不宜继续演进 | Legacy/Retire |
| `media-platform` | FastAPI + SQLAlchemy + Celery + MinIO + SQLAdmin；README 自称 Phase0 骨架、13 models | 旧一代平台骨架，不应恢复为第二主平台 | Freeze / Extract |
| `city-converged-media-platform` | Python3.13/FastAPI/SQLAlchemy/Alembic + SRS/FFmpeg + Vue3；文档宣称等保/大规模能力，但 README 版本规划仍显示 MVP/计划性指标 | 大量“平台级声明”高于可验证实现，存在烂尾/过度设计风险 | Extract / Freeze |
| `video-management-system` | Python/FastAPI/SQLAlchemy + Vue3 + Celery；README 宣称上传/转码/AI/HLS/监控全套，但项目规模很小且文档内容存在重复/过时结构 | 典型早期视频管理全栈原型 | Extract / Freeze |

## 3. 第一轮最终结论

当前组合不是“旧项目太多”，而是“完成度差异太大”。必须把仓库分成：

### A. 真实核心

`news-media-system`, `VBMF`, `live-platform`, `YimengSpirit-Multimodal`。

### B. 必须合并的重复产品

`lamice`, `media-ai-platform`, `lamice-platform`。

这里实际上不是两套，而是**三代 Creative/LAMICE 技术路线**：

```text
waoowaoo/Next+Prisma+BullMQ
        ↓
lamice/Next+Prisma+BullMQ
        ↓
lamice-platform/FastAPI+SQLAlchemy+Vue
```

后续必须选一条生产主线，其他两代只做资产迁移；绝不能三线并进。

### C. 专业能力

`video-shot-detection`, `video-compression-system`。

只保留 Engine 能力，不继续建设独立产品壳。

### D. 数据与研究

`ai-spider-annotation`, `yimengjingshen`。

分别进入 Data Studio 与 Model Research Lab。

### E. 消费端

`xiao-opera-miniapp`，重做服务接入和 AI 闭环，保留 UX 资产。

### F. 历史

`YimengHeart`, `media-platform`, `city-converged-media-platform`, `video-management-system`。

原则上 Freeze/Extract，而不是继续堆功能。

## 4. 新的“完成度”认定

从本报告开始，母架构库统一使用：

- **Claimed**：文档声称拥有。
- **Implemented**：源码存在且能定位到调用链。
- **Integrated**：至少一个真实跨模块链路闭环。
- **Verified**：有自动化/真实环境证据。
- **Production**：真实部署、监控、失败恢复和运维闭环成立。

因此一个项目可以出现：

```text
Claimed = 90%
Implemented = 60%
Integrated = 35%
Verified = 20%
Production = 0%
```

这比传统“功能清单 90% 完成”更加真实。

## 5. 下一阶段

继续逐库下钻到：

1. DB schema 与 migration。
2. API route + DTO + error model。
3. Job/task state machine。
4. Storage/Artifact lineage。
5. Auth/identity。
6. Frontend route 与核心交互。
7. Test/CI/runtime evidence。

每个仓库完成后必须进入单独的 archaeology report 和 migration decision。