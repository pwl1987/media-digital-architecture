# Repository Archaeology Method

> 面向多代媒体/AI项目的统一考古与取舍方法

## 目标

考古不是评审“代码写得漂不漂亮”，而是回答：

- 项目实际解决了什么问题？
- 哪些功能是真闭环，哪些只是声明、Mock、Demo 或半成品？
- 哪些技术资产值得继承？
- 哪些架构会把历史债务带入新平台？
- 项目最终应该继续、重建、抽取、冻结还是退役？

## Evidence Chain

```text
README / PRD
    ↓
Repository Tree
    ↓
Entry Points
    ↓
Schema / Storage
    ↓
API / Command
    ↓
Worker / Runtime
    ↓
Result / Artifact
    ↓
Test / CI
    ↓
Real Environment
```

只有链条形成闭环，完成度才可以上调。

## Completion Levels

| Level | Meaning |
|---|---|
| C0 | 概念/文档/原型 |
| C1 | 有源码或页面，但没有端到端证据 |
| C2 | 局部可执行，有测试或单路径验证 |
| C3 | API + persistence + execution + failure handling + tests |
| C4 | 真实环境验收、可重复部署或已有真实使用 |

## Archaeology Dimensions

每个仓库固定检查：

### Product

- 目标用户
- 核心场景
- 用户入口
- 主流程
- 完成/失败/恢复流程
- 实际用户证据

### Domain

- 一级对象
- 对象关系
- 状态机
- ID/版本
- 数据所有权

### Technology

- frontend
- backend
- database
- queue
- object storage
- runtime
- model/provider
- deployment

### Reliability

- timeout
- retry
- idempotency
- cancellation
- reconciliation
- health/readiness
- backup/recovery

### Security

- authentication
- authorization
- secrets
- upload validation
- SSRF/path traversal
- audit
- tenant isolation

### Verification

- unit tests
- integration tests
- e2e
- CI
- smoke
- real-service verification

### Reuse Value

给每项资产单独判断：

- domain value
- algorithm value
- infrastructure value
- UX value
- test value
- documentation value

## Disposition Matrix

```text
High business value + high technical value
    → RECOVER / HARDEN

High business value + low technical value
    → REBUILD

Low business value + high technical value
    → EXTRACT

Low business value + low technical value
    → FREEZE / RETIRE
```

## Anti-Patterns

### 1. Code Volume Bias

代码多不代表价值高。

### 2. Test Count Bias

测试数量不等于产品闭环。

### 3. README Completion Bias

README 的“已完成”只能证明作者声明。

### 4. Architecture Document Bias

设计文档成熟不代表 runtime 完成。

### 5. Demo Bias

能生成一次结果不代表具有可靠任务生命周期。

### 6. Rewrite Bias

发现架构问题后直接新建仓库，不得作为默认动作。

## Required Archaeology Record

每个项目报告至少包含：

```yaml
repository:
  name:
  default_branch:
  observed_at:

classification:
  role:
  lifecycle:
  health:
  completion_level:
  evidence_level:

product:
  target_users: []
  core_flows: []
  broken_flows: []

assets:
  domain_assets: []
  code_assets: []
  ux_assets: []
  research_assets: []

risks:
  critical: []
  high: []
  medium: []

architecture:
  canonical_objects: []
  provided_capabilities: []
  consumed_contracts: []
  forbidden_dependencies: []

recommendation:
  disposition:
  destination:
  migration_notes: []
```

## Update Rule

考古结论必须写入母架构仓库；当后续获得更强证据时，允许降低或提高评级，但必须保留变更理由。