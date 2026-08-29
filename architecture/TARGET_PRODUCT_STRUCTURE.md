# Target Product Structure — Draft 0.1

## 1. Product principle

目标不是把所有旧仓库拼成一个“超级系统”，而是让用户看到一个统一的媒体数字智能产品家族，让专业运行时在后台各司其职。

> One Experience, One Domain Language, Multiple Specialized Runtimes.

## 2. Proposed top-level experience

建议主题产品暂定：`Media Digital Platform` / `数字媒体智能中心`。

主题平台负责：

- SSO / identity
- global navigation
- workspace
- global search
- notifications
- global task center
- module registration
- cross-system deep links
- common design system
- unified error/loading/status semantics

它不拥有内容、广播、AI 模型或创意资产的全部业务事实。

## 3. User-facing modules

```text
数字媒体智能中心
├── 内容
├── 媒资
├── AI 智能
├── 知识
├── 创意
├── 直播
├── 广播
├── 数据
└── 运维
```

模块只是体验入口；真正业务状态由专业系统拥有。

## 4. Module ownership

| Experience | System owner | Primary role |
|---|---|---|
| 内容 | `news-media-system` | Content Platform |
| 媒资 | `news-media-system` + Processing Engines | Asset / Content |
| AI 智能 | `YimengSpirit-Multimodal` | Intelligence |
| 知识 | Yimeng Intelligence | Knowledge / Evidence |
| 创意 | `media-ai-platform` target | Creative Platform |
| 创意工作台 | `LAMICE` target | Creative Studio |
| 直播 | `live-platform` | Live Operations |
| 广播 | `VBMF` | Broadcast Runtime |
| 数据 | `ai-spider-annotation` target | Data Studio |
| 研究 | `yimengjingshen` | Research Lab |
| 公众文化 | `xiao-opera-miniapp` | Consumer App |

## 5. Shell before micro-frontends

第一阶段不要立即引入 Module Federation 等复杂微前端技术。

优先使用：

```text
Unified Shell
  ↓
SSO
  ↓
Module Registry
  ↓
Deep Link / reverse proxy / application route
  ↓
Specialized Application
```

在统一契约稳定之前，微前端会放大边界问题，而不是解决边界问题。

## 6. Experience principles

### Business

围绕“工作”而不是“AI 能力”组织界面。

例如：

```text
整理采访
→ ASR
→ 摘要
→ 人物
→ 重点
```

而不是让用户自己理解 ASR、LLM、Embedding 等技术概念。

### AI

AI 页面必须优先展示：

- context
- evidence
- source
- provenance
- task status
- model/version when relevant

不把“聊天气泡”当作唯一 AI 产品范式。

### Creative

创作页面应围绕：

```text
Project
→ Script
→ Character / Scene
→ Storyboard
→ Timeline
→ Generation
→ Review
→ Render
```

### Consumer

面向公众的产品应以文化内容发现、观看、学习、互动、创作体验为中心，而不是暴露后台 AI 平台概念。

## 7. Product boundaries

禁止主题平台：

- 直接操作 DeckLink/GStreamer/FFmpeg；
- 直接读取专业系统数据库；
- 自己复制 Creative Project/Media/Task 等业务事实；
- 自己维护第二套 AI provider registry；
- 自己维护第二套媒体处理 pipeline。

## 8. Target outcome

用户层：一个产品家族。

开发层：多个专业仓库。

数据层：明确 owner + Contract。

运行层：专业 runtime 各自优化。

治理层：`media-digital-architecture` 统一规则。
