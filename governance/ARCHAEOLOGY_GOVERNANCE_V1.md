# Archaeology Governance V1

> 项目考古不是代码清理，而是对历史工程资产进行价值、风险和归属判断。

## 1. 四种对象必须分开

- **Product**：面向真实用户的完整业务能力。
- **Platform**：承载多个产品/领域的共享控制与基础能力。
- **Engine**：单一专业能力，可被多个上层系统调用。
- **Research / Prototype**：验证思想、算法或体验的实验资产。

代码仓库只是承载形式，不决定对象类型。

## 2. 六维考古模型

每个仓库按 0-5 级分别评估：

| 维度 | 0 | 5 |
|---|---|---|
| Product Value | 无真实场景 | 核心业务 |
| Domain Value | 无独特领域资产 | Canonical domain owner |
| Technical Value | 无可复用价值 | 可成为平台/引擎基线 |
| Completion | Demo | 完整生产闭环 |
| Reliability | 未验证 | 真实环境 E4 |
| Duplication Risk | 独特 | 与多个项目重复 |

总分不是自动决定命运；**高重复风险会触发重构，即使总分高也不能并行继续发展。**

## 3. 处置决策

### KEEP
继续作为正式系统，但必须遵守母架构与契约。

### HARDEN
核心价值明确，但先补可靠性、安全性、运维与验证。

### CONSOLIDATE
业务价值明确，但与其他项目存在同域重复；进入统一产品/平台。

### REBUILD
业务价值高、历史技术债高；保留领域与需求资产，重建运行时。

### EXTRACT
项目整体不值得保留，但存在值得下沉的算法、引擎、Schema、UX 或其他资产。

### FREEZE
停止新增功能，仅保留只读、迁移、兼容或必要修复。

### RETIRE
停止运行和维护；在满足审计/合规要求后归档。

## 4. 禁止的错误修复方式

1. 不因为 README 功能清单长就继续开发。
2. 不因为测试数量高就认定产品完成。
3. 不因为 UI 能操作就认定后端闭环。
4. 不因为 API 返回 200 就认定业务成功。
5. 不因为架构文档成熟就认定运行时已经成熟。
6. 不把历史项目的临时 workaround 继承到新平台。
7. 不为消灭技术栈差异而破坏专业 runtime。
8. 不允许同一 canonical object 在多个系统各自定义一份事实源。

## 5. 资产保留优先级

优先保留：

1. 已在真实环境验证的算法/引擎。
2. 已真实使用的业务规则。
3. 高质量领域数据与数据血缘。
4. 用户真实使用过的 UX 流程。
5. 可验证的 Schema/API 合同。
6. 测试、验收脚本和故障案例。
7. 最后才是目录结构和代码组织方式。

## 6. 每次考古必须输出

- Archaeology Report
- Evidence Matrix
- Functional Gap List
- False-Completion List
- Domain/Capability Ownership
- Reusable Asset Inventory
- Migration Destination
- Final Disposition
- Open Questions

## 7. 决策生命周期

```text
DISCOVER
  ↓
EVIDENCE
  ↓
ASSESS
  ↓
DECIDE
  ↓
MIGRATE / EXTRACT / HARDEN
  ↓
VERIFY
  ↓
FREEZE / RETIRE
```

任何处置在迁移后必须重新验证；“已经迁移”不是完成状态。

## 8. 与 AI Coding Agent 的关系

AI Agent 进入旧仓库时必须先读取该仓库的 `repo-manifest` 和本文件对应的 archaeology record。

如果仓库状态为 `FREEZE` / `RETIRE`，Agent 默认不得新增产品功能。

如果仓库状态为 `CONSOLIDATE` / `REBUILD`，Agent 必须以目标平台 Contract 为准，而不是继续扩大历史实现。

如果仓库状态为 `EXTRACT`，Agent 只应修改抽取目标，不应恢复被淘汰的外围平台功能。