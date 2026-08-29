# ADR-001 — Unified Experience Platform

- Status: PROPOSED
- Date: 2026-08-29
- Scope: entire media digital ecosystem

## Context

当前生态存在多个用户入口：新闻/媒资平台、Yimeng AI、AI 视频创作、直播运营、文化小程序和多个研究/工具型前端。它们可以保持专业独立，但如果各自维护用户入口、导航、身份、设计语言和任务呈现，最终用户会感知为多个互不相关的产品。

## Decision

建立一个独立的**主题主平台**（working name: `media-digital-platform`）作为 Experience / Identity / Navigation / Workspace Shell。

它不是新的 CMS，不复制 `news-media-system` 的业务事实源，也不替换专业运行时。

主题主平台负责：

- 统一登录/SSO、用户会话与组织上下文
- 统一全局导航与工作空间
- 统一搜索入口和跨系统任务中心
- 统一通知、消息、最近使用、收藏等体验级能力
- 统一 Design Tokens 与核心交互语言
- 通过正式 API/Contract 进入各专业系统

专业系统负责自己的业务功能：

- `news-media-system`：内容、媒资、工作流、发布及业务 AI 控制面
- `YimengSpirit-Multimodal`：领域 Intelligence / Knowledge / RAG / Model
- `media-ai-platform`：AI 视频生产平台
- `LAMICE`：Creative Studio
- `live-platform`：Live Operations
- `VBMF`：Broadcast Runtime/Fabric
- Media engines：专业媒体处理

## Why not a monolith

统一体验不等于统一运行时。

不采用：

- 所有源码合并到一个 repository
- 所有服务共享一个数据库
- 所有系统强制使用同一 runtime
- UI 直接访问其它系统数据库
- 一个 giant backend 包含 Live/VBMF/AI/Creative 全部实现

采用：

```text
Unified Experience Shell
        ↓
Business / Intelligence / Creative / Live APIs
        ↓
Specialized Systems
```

## Initial implementation strategy

第一阶段不采用微前端平台复杂化方案。优先使用统一 SSO、统一导航、统一 design system 和标准路由/链接接入，逐步把专业应用纳入同一工作空间。

只有当路由、部署、权限和运行时边界已经稳定，并且确实需要无缝嵌入多个独立前端时，才评估 micro-frontend。

## Consequences

### Positive

- 用户获得单一产品心智
- 专业系统继续保持独立演进
- 可以渐进迁移历史项目
- 设计系统和身份体系有唯一入口

### Negative

- 新增一个体验层
- 需要建立 SSO / navigation / cross-system contract
- 专业应用需要适配统一 shell

### Guardrails

主题平台不得创建下列第二事实源：

- Content
- Media Asset
- Knowledge
- Model
- Job execution
- Broadcast state

这些事实由专业系统拥有。
