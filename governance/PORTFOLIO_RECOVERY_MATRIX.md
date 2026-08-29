# Portfolio Recovery Matrix — Draft 0.1

## 1. Purpose

本矩阵用于处理现有项目“代码很多但功能不完整、长期未完成、只有部分能力可用、架构与现状不一致”的情况。

**核心原则：不要默认修复旧项目；先判断是否值得救。**

代码量、提交数量、文档数量、项目年龄都不是继续投入的充分理由。

## 2. Assessment dimensions

每个仓库至少评估以下维度：

| 维度 | 关注点 |
|---|---|
| Business Value | 是否解决真实业务问题，是否存在明确用户 |
| User Reality | 是否有真实用户、真实使用路径、真实反馈 |
| Functional Completeness | 核心业务闭环是否完成，而不是页面/接口数量 |
| Runtime Health | 能否稳定启动、部署、升级、恢复 |
| Test Evidence | 单测、集成、E2E、真实环境验证 |
| Data Reality | 是否有真实数据、数据生命周期是否完整 |
| Architecture Fitness | 是否符合当前目标架构 |
| Code Quality | 可维护性、边界、重复、历史债务 |
| Reusable Assets | 数据模型、算法、引擎、UI、脚本等可抽取价值 |
| Security | Secret、Auth、SSRF、文件处理、权限边界 |
| Operational Cost | 维护复杂度、依赖数量、运行资源 |
| Strategic Fit | 是否属于未来核心能力域 |

## 3. Decision classes

### A — Recover

条件：

- 业务价值高
- 核心闭环接近完成
- 当前架构仍可接受
- 有足够真实代码/数据/测试证据

策略：修复关键断点，补齐闭环，进入目标架构。

### B — Rebuild

条件：

- 业务价值高
- 当前实现架构债务过大
- 继续修补的成本高于重建

策略：保留业务事实和可复用资产，在新架构中重建；旧仓库冻结为迁移源。

### C — Extract

条件：

- 独立产品价值有限
- 存在明确高价值算法/引擎/数据/脚本

策略：提取能力为 Engine/Library/Artifact，原项目停止扩张。

### D — Freeze

条件：

- 当前仍有历史/演示/兼容价值
- 不值得继续投入

策略：只接受安全修复和必要兼容变更。

### E — Retire

条件：

- 低业务价值
- 低复用价值
- 无真实用户或已被新系统取代

策略：建立迁移/归档记录后正式退役。

## 4. Evidence rules

结论必须优先由证据支持：

```text
代码入口
Schema
API routes
Tests
CI
Docker
Runtime logs
真实数据
实际 UI flow
```

README、roadmap、issue、计划文档只能作为线索，不能单独证明功能已经完成。

## 5. “完成”定义

一个功能只有在以下条件同时满足时，才可以标记为 COMPLETE：

1. 用户入口存在；
2. API/服务入口存在；
3. 数据模型/状态存在；
4. 正常路径可运行；
5. 失败路径有明确语义；
6. 持久化/产物可验证；
7. 至少有自动化测试或真实环境验证；
8. 文档描述与实际行为一致。

只有“按钮存在”“函数存在”“mock 能返回结果”都不算完成。

## 6. Common unfinished patterns

### Mock completion

页面和 API 已经存在，但返回固定/随机/模拟数据。

### UI-first completion

页面很多，但真正的业务状态机、持久化和错误恢复缺失。

### API-first completion

接口数量很多，但没有真实用户流程和完整端到端闭环。

### Architecture-first completion

架构文档、抽象层、provider、registry 很完整，但真实数据/模型/生产流程没有闭环。

### Demo-to-product gap

Demo 可以跑，但缺少 auth、quota、audit、retry、observability、backup、migration、security 等生产要求。

### Legacy accretion

为了“兼容以前版本”持续增加字段、URL、入口和双写，导致没有明确事实源。

## 7. Current portfolio provisional assessment

| Repository | Provisional disposition | Reason |
|---|---|---|
| `news-media-system` | Recover / Core | 当前最接近长期业务主平台；应在现有基础上收敛架构 |
| `YimengSpirit-Multimodal` | Rebuild / Continue selectively | AI 方向战略价值高，但当前应停止无边界堆平台功能，转向 Intelligence Core |
| `media-ai-platform` | Rebuild / Consolidate | Creative runtime 很重，与 LAMICE 存在明显重复 |
| `LAMICE` | Recover as Studio / Consolidate | 产品体验价值高，但不应继续单独维护第二套 Creative backend |
| `VBMF` | Recover / Core Runtime | 专业广播实时基础设施，保持独立运行时 |
| `live-platform` | Recover / Core | 作为 Live Operations 保持专业边界 |
| `video-shot-detection` | Extract / Engine | 能力边界清晰，应标准化为 Engine |
| `video-compression-system` | Extract / Engine | 质量/压缩能力清晰，应作为 Processing Engine |
| `ai-spider-annotation` | Rebuild / Data Studio | 数据价值高，但不应继续成为独立业务孤岛 |
| `yimengjingshen` | Lab / Extract | 研究价值高，生产边界必须清楚 |
| `xiao-opera-miniapp` | Recover / Consumer App | 保留用户端定位，AI 能力通过 Intelligence API 接入 |
| `media-platform` | Freeze / Extract | 旧架构迁移来源，不再并行建设主平台 |
| `YimengHeart` | Freeze / Retire | Legacy compatibility 后逐步退出 |

**注意：以上是初步判断，不等同于最终尸检结论。** 每个项目必须经过逐仓库证据审计后才能升级/降级。

## 8. Recovery order

建议优先处理对未来主平台影响最大的项目，而不是历史上最老的项目：

```text
1. news-media-system
2. YimengSpirit-Multimodal
3. media-ai-platform + LAMICE
4. live-platform
5. VBMF
6. Processing Engines
7. Data Studio
8. Consumer / Legacy
```

## 9. Stop-the-line conditions

出现以下任一情况，不允许继续堆新功能，应先做修复/重构：

- 核心用户流程无法闭环；
- 两个系统同时维护同一事实源；
- 生产路径仍依赖 mock/fake；
- 数据无法追溯来源；
- Job 状态不可解释；
- 失败后无法恢复；
- API 与 UI 对同一对象存在不同语义；
- 安全边界不明确；
- 运行依赖无法重现；
- 关键功能没有真实环境验证。

## 10. Rule for future development

新功能必须先回答：

```text
它属于哪个 Domain？
谁拥有它？
哪个系统实现它？
哪个 Contract 对外？
哪个 Artifact 产生？
哪个 Job 承担执行？
如何测试？
如何回滚？
```

如果这些问题没有答案，不进入实现阶段。
