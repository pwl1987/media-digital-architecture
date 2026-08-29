# Project Completion Gate — Draft 0.1

## 1. Problem

历史项目普遍存在“页面完成、接口完成、代码完成，但业务没有完成”的情况。因此项目完成度必须按端到端业务切片判断。

## 2. Feature completion gate

一个核心功能必须通过以下八道门：

```text
G1 User Intent
  ↓
G2 UX Entry
  ↓
G3 API / Command
  ↓
G4 Domain State + Persistence
  ↓
G5 Execution / Worker / Runtime
  ↓
G6 Result / Artifact
  ↓
G7 Failure / Retry / Recovery
  ↓
G8 Automated or Real-Environment Verification
```

任一关键环节缺失，功能只能标记为 `partial`，不能标记为 `complete`。

## 3. Core flow verification

每个项目至少应有 3–10 条最关键业务旅程作为 Golden Journeys。

### Example: media analysis

```text
Upload Media
→ Asset Registered
→ Analysis Job Created
→ Worker Executes
→ Shot/ASR/OCR/VLM Artifacts Produced
→ Result Persisted
→ UI Shows Progress/Result
→ Failure Can Retry
→ Evidence/Test Recorded
```

### Example: AI generation

```text
Creative Request
→ Task
→ Job
→ Generation
→ Artifact
→ Preview
→ Persist
→ Retry/Cancel
→ Audit
```

## 4. Anti-fake completion checks

以下情况不得标记 Complete：

- UI 使用假数据；
- API 使用固定响应；
- TODO/NotImplemented 路径仍位于主流程；
- 只验证 HTTP 200，没有验证结果；
- 只跑单测，没有验证真实 worker；
- 输出没有持久化；
- 结果 URL 存在但 Artifact identity 不存在；
- 失败后只能刷新页面；
- 数据库状态与 UI 状态可能分叉；
- 文档描述的能力没有对应代码入口。

## 5. Release candidate gate

一个项目进入 RC 前至少需要：

- 核心 Golden Journeys 全部通过；
- 正常路径与主要异常路径均验证；
- migration 可重复执行；
- 配置缺失能 fail-fast；
- 关键 secret 不进入仓库；
- 健康检查和 readiness 有明确语义；
- 日志包含 trace/request/job correlation；
- 主要产物可追溯；
- 回滚/恢复策略已验证；
- 文档与实际行为一致。

## 6. Project-level status

建议把项目状态拆成：

```text
PROTOTYPE
→ FUNCTIONAL
→ INTEGRATED
→ OPERATIONAL
→ RELEASE_CANDIDATE
→ PRODUCTION
```

不要用“80%完成”这类无法验证的表述替代状态。
