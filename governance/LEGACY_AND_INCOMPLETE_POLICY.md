# Legacy & Incomplete Project Governance — Draft 0.1

## 1. Core judgment

当前项目群存在一个必须正视的现实：一批历史仓库并非“可直接继承的成熟系统”，而是不同完成度的实验、MVP、阶段性工程或烂尾项目。

因此不得把“已有代码”默认等同于“现行标准”，也不得因为某个仓库历史上投入较多就继续扩张其职责。

**代码存在 ≠ 功能完成 ≠ 架构正确 ≠ 可以复用 ≠ 应继续维护。**

## 2. Project health taxonomy

每个仓库必须同时记录两个维度：

### Lifecycle

- `ACTIVE` — 当前业务继续使用并有明确路线
- `CONSOLIDATING` — 能力正在迁移/收敛
- `FROZEN` — 停止新增功能，只接受必要修复
- `LEGACY` — 仅兼容或作为迁移来源
- `RETIRED` — 已正式退出

### Health

- `GREEN` — 核心闭环完整，有持续验证
- `YELLOW` — 可运行但存在明显缺口
- `ORANGE` — 只有部分闭环，不能作为平台事实源
- `RED` — 烂尾/实验/大量 Mock/功能断裂，不得扩张

Lifecycle 与 Health 相互独立。例如一个 `ACTIVE + RED` 项目必须先做 recovery，不应直接进入 feature development。

## 3. Definition of “incomplete”

出现以下任一情况，应标记 `ORANGE/RED`：

- README/规格明显大于实际实现
- 首页可展示，但核心业务闭环没有完成
- 大量 TODO / NotImplemented / mock / simulate
- 数据模型已经建立但实际流程未打通
- API 存在但前端/worker/下游没有真实消费者
- 训练能 dry-run，但没有可信业务评测
- “支持”某媒体格式/能力，但只有入口没有端到端验证
- 有多个 parallel implementation，实际没有唯一 owner
- 测试只覆盖结构，不覆盖真实业务结果
- 生产部署方式没有经过真实环境验证

## 4. No automatic inheritance

历史项目中的以下内容均不得自动成为新系统标准：

- 技术栈
- 数据库 schema
- API 设计
- UI patterns
- 配置系统
- 权限模型
- Job state machine
- Provider model
- 命名

只有经过 Architecture Review 并被纳入 Canonical Contract 的内容，才能成为新项目的标准。

## 5. Recovery before expansion

对 `ORANGE/RED` 项目，优先级必须是：

```text
Truth discovery
  ↓
Feature inventory
  ↓
Broken-flow identification
  ↓
Value assessment
  ↓
Keep / migrate / rewrite / retire
  ↓
Only then implement
```

禁止通过“继续加功能”掩盖未完成的基础闭环。

## 6. Recovery classes

### Preserve

核心域模型正确、实现质量尚可、与目标架构一致。

### Extract

项目本身不再作为独立产品，但内部有可复用 Engine/Algorithm/Adapter。

### Rebuild

业务价值明确，但现有代码与目标架构差距过大。

### Freeze

有历史价值或仍有少量用户，但不值得继续投资。

### Retire

功能已被新系统覆盖，且不存在必须保留的运行义务。

## 7. Current portfolio interpretation

初步审计认为：

- `news-media-system`：核心建设中，优先保护其 Business Control Plane 价值。
- `YimengSpirit-Multimodal`：核心潜力高，但必须完成从 scaffold 到产品闭环的收敛。
- `VBMF`：专业实时基础设施，不按普通业务系统标准评价。
- `live-platform`：专业 Live Operations，需评估真实业务闭环后继续收敛。
- `media-ai-platform`：功能与工程投入较大，但与 `LAMICE` 存在严重边界重复，先整合后扩张。
- `LAMICE`：Creative UX/Studio 价值高，但不能继续复制平台基础设施。
- `video-shot-detection`：高价值 Engine 候选，应脱离产品 UI 生命周期。
- `video-compression-system`：高价值 Processing Engine 候选，应从单一应用思维转为标准能力。
- `ai-spider-annotation`：有数据运营价值，但应脱离临时 SQLite/导出式工作流，进入统一 Dataset/Annotation Contract。
- `yimengjingshen`：Research Lab；实验成功不等同于生产能力完成。
- `xiao-opera-miniapp`：Consumer Application；AI 生成链路目前不能视作成熟生产能力，必须以真实服务闭环重新验收。
- `media-platform`：主要作为迁移来源，不再作为第二套业务主平台。
- `YimengHeart`：Legacy；原则上只保留兼容能力。

这些是当前审计结论，不是永久评级；正式评级必须附真实证据。

## 8. Completion scorecard

未来每个核心项目必须至少报告：

```text
Business Closure
Functional Coverage
Real Implementation Coverage
Integration Coverage
Data Readiness
Test Readiness
Deployment Readiness
Observability
Security
UX Readiness
Documentation Truthfulness
```

禁止仅用“代码量/commit 数/测试数量”衡量成熟度。

## 9. Portfolio rule

**新能力优先进入成熟的 Canonical Owner；不要因为旧项目已有半套代码，就再复制半套实现。**

当多个烂尾项目共同覆盖一个领域时，不做“平均融合”，而做“择优归并”：

```text
Find the best domain model
Find the best implementation
Find the best UX
Find the best operational model
        ↓
One Canonical Owner
        ↓
Adapters for legacy systems
```

## 10. Required repository manifest

每个纳入生态的仓库最终应包含一份机器可读 `architecture-manifest.yaml`，至少描述：

- `system_id`
- `role`
- `lifecycle`
- `health`
- `canonical_domains`
- `provided_capabilities`
- `consumed_contracts`
- `owned_objects`
- `forbidden_dependencies`
- `runtime`
- `data_store`
- `task_runtime`
- `deployment`
- `last_verified_commit`

这样 AI coding agent 和人工维护者才能区分“当前事实”和“历史遗留”。

## 11. Non-negotiable principle

> **不要修复一个你还没有判定是否值得保留的系统。**
>
> 先判断它的业务价值、域模型价值、代码资产价值和迁移成本，再决定修、拆、并、冻、废。
