# Repository Archaeology Method

## 目标

把历史仓库从“项目”还原成四类可判断对象：

1. 产品事实
2. 技术实现
3. 可复用资产
4. 历史债务

最终输出不是代码数量，而是处置建议：`KEEP / REBUILD / EXTRACT / FREEZE / RETIRE`。

## 证据等级

### E0 — 声明

README、PRD、注释、roadmap 中声称存在。

### E1 — 静态实现

源码、Schema、API、配置、Worker 等已经存在对应实现。

### E2 — 自动验证

Unit / Integration / Contract / Build / Typecheck 等通过。

### E3 — 真实运行

在对应依赖、媒体、GPU、浏览器或设备环境中实际跑通。

### E4 — 真实业务闭环

真实用户场景从入口到结果/Artifact/持久化/恢复均可完成，并具备回归证据。

**只有 E4 才允许把能力称为生产完成。**

## 六个检查维度

### Product

- 核心用户是谁？
- 核心任务是什么？
- 主流程是否闭环？
- 是否存在大量“页面有、后端没有”或“后端有、入口没有”？

### Domain

- 对象定义是什么？
- 谁拥有对象？
- ID 如何产生？
- 是否与 Canonical Objects 冲突？

### Runtime

- API / worker / process 是否真的存在？
- 失败、重试、取消、恢复是否有语义？
- 是否依赖未声明的本地环境？

### Data

- Schema 是否实际存在？
- Migration 是否可重复？
- 文件 / URL / Asset / Artifact 是否区分？
- 数据是否可追溯？

### UX

- 用户路径是否完整？
- Loading / empty / error / retry 是否完整？
- 页面是否只是 demo shell？

### Engineering

- build / test / lint / CI 是否可信？
- Docker 是否与 README 一致？
- 默认配置是否安全？
- 版本是否可复现？

## “烂尾”判定

以下任一项只能把功能标记为 partial：

- 只有 UI mock；
- 只有 API skeleton；
- 返回固定/模拟结果；
- 只有 happy path；
- 核心状态字段缺失；
- 外部依赖没有真实运行验证；
- 结果没有持久化为 Artifact；
- 失败后无法恢复；
- 测试只测函数而不测用户闭环。

## 复用价值分类

### Product Asset

产品流程、信息架构、UX、领域经验。

### Domain Asset

Schema、对象定义、状态机、业务规则。

### Engine Asset

算法、FFmpeg/GStreamer pipeline、GPU代码、处理器。

### Platform Asset

认证、存储、队列、可观测、审计、配置、部署。

### Research Asset

实验、数据集、模型权重、benchmark。

### Debt

旧兼容层、重复实现、mock、错误抽象、未完成分支。

## 处置规则

```text
E4 + 高价值 + 架构兼容       → KEEP
高业务价值 + 技术债高        → REBUILD
独立算法/引擎价值高           → EXTRACT
价值有限 + 可参考             → FREEZE
低价值 + 无唯一资产           → RETIRE
```

## 禁止的考古偏差

- 不因为仓库很大而判定值得保留。
- 不因为测试数量多而判定业务完整。
- 不因为 README 写“production”而默认生产级。
- 不因为文档很多而默认架构成熟。
- 不因为某技术很新而强行进入新架构。
