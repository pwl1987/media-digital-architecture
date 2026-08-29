# Domain Model — Draft 0.2

本文件定义跨仓库共同语言，重点解决当前 `Project / Media / Asset / Shot / Clip / Job / Artifact` 语义漂移。

## 1. 核心对象

### Identity / Business

- `Organization` — 租户/机构边界。
- `User` — 身份主体。
- `Site` — 内容发布站点/渠道。
- `ContentProject` — 新闻/内容生产项目。
- `CreativeProject` — AI 创作项目。
- `BroadcastSession` — 广播运行会话。
- `ResearchExperiment` — 模型研究实验。

### Content / Media

- `Content` — 可编辑、审核、发布的内容对象。
- `Asset` — 可管理的内容/媒体资产身份。
- `Artifact` — 处理、分析、生成产生的具体产物。
- `Media` — 具有媒体语义的 Asset/Artifact 类型或视图。

### Intelligence

- `Knowledge` — 可检索/结构化知识。
- `Evidence` — 支撑知识或回答的证据。
- `Generation` — AI 生成过程及输入输出。
- `Model` — 可注册、评估和部署的模型版本。
- `Dataset` — 数据集版本。

### Execution

- `Job` — 异步可追踪计算。
- `Session` — 持续状态运行上下文。

## 2. Asset / Artifact 分层

```text
Asset
  │ 业务身份：我拥有什么内容
  ▼
Artifact
  │ 某次处理/分析/生成产生的具体结果
  ▼
KnowledgeArtifact / DatasetArtifact / DeliveryArtifact ...
```

URL、文件路径、bucket key 不能成为业务主键。

## 3. 领域限定命名

### 视频分析

`VideoShot`：现实世界视频经过检测得到的镜头结果。

### 视频创作

`StoryboardShot`：剧本/分镜中的镜头设计。

`StoryboardPanel`：分镜画面板。

`TimelineClip`：时间线上的编辑片段。

禁止把这些对象在跨域 API 中都简称为 `Shot` 或 `Clip`。

## 4. Project 语义

当前多个项目都有无上下文的 `Project`。

规则：跨系统公共 API 中不得只依赖裸 `Project`。必须带领域语义：

```text
ContentProject
CreativeProject
ResearchExperiment
BroadcastSession
```

## 5. Provenance

任何 Artifact、Knowledge、Dataset Sample、Model Artifact 都必须能够回答：

```text
Who/what created it?
From which input?
Which version?
When?
Under which policy/configuration?
```

建议最小关联：

```text
artifact_id
parent_artifact_ids
producer
producer_version
created_by
created_at
metadata
```

## 6. 生命周期

### Asset

```text
registered → active → superseded/archived → deleted
```

### Artifact

```text
created → validated → published/consumed → archived
```

### Job

```text
queued → running → succeeded | failed | canceled
```

具体状态可按领域扩展，但必须保持终态语义一致。

## 7. 关系总图

```text
ContentProject / CreativeProject
             │
             ▼
          Content
             │
             ▼
           Asset
             │
       ┌─────┴─────┐
       ▼           ▼
   Processing    Generation
       │           │
       └─────┬─────┘
             ▼
          Artifact
             │
       ┌─────┴─────┐
       ▼           ▼
   Knowledge    Dataset
       │           │
       └─────┬─────┘
             ▼
           Model
```

这是目标语义图，不是当前数据库的直接映射；后续必须通过实际 Schema Audit 决定迁移字段与兼容层。
