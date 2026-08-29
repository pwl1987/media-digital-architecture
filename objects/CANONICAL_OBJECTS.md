# Canonical Objects — Draft 0.1

本文件先定义跨系统共同语言。具体字段、生命周期和 ownership 在后续 Schema Audit 中继续冻结。

## 1. 一级 Canonical Objects

| Object | 含义 | 建议事实源 |
|---|---|---|
| Organization | 组织/租户边界 | Business Platform |
| User | 用户身份 | Identity / Business Platform |
| Site | 发布站点/业务渠道 | Business Platform |
| Project | 业务项目容器 | Business/Creative domain |
| Content | 编辑/发布内容 | News Media |
| Asset | 可管理的媒体/内容资产 | Asset Registry / News Media |
| Artifact | 某次处理、生成或分析产生的具体产物 | Artifact Registry |
| Media | 具有媒体语义的 Asset/Artifact 类型 | Media domain |
| Session | 持续的直播/广播运行会话 | Live/Broadcast domain |
| Job | 异步、可追踪的计算请求 | Job Control Plane |
| Knowledge | 结构化或检索型知识 | Intelligence Plane |
| Dataset | 训练/评测数据集合 | Data/Research Plane |
| Model | 可注册、可评测、可部署的模型 | Model Registry |
| Generation | AI 生成过程及其输入输出关系 | Intelligence/Creative |
| Evidence | 支撑知识、回答或生成 grounding 的证据 | Intelligence Plane |

## 2. Identity 原则

- `id` 是业务身份，不等于 URL。
- Object Storage URI 只是 locator。
- 同一个 Artifact 可以拥有多个 delivery URL。
- 派生结果必须保留 provenance。
- 删除/替换存储位置不应改变业务身份。

## 3. Artifact

建议所有媒体处理、AI 分析和生成结果最终落成 Artifact：

```json
{
  "artifact_id": "artifact-...",
  "type": "video",
  "media_type": "video/mp4",
  "uri": "s3://...",
  "checksum": "...",
  "size": 0,
  "parent_artifact_ids": [],
  "producer": "shot-engine",
  "producer_version": "...",
  "metadata": {},
  "created_at": "..."
}
```

以上为语义草案，不是最终 API Schema。

## 4. 领域限定名称

禁止不同领域共享一个含义不清的 `Shot`、`Clip`、`Project`。

建议使用：

- `VideoShot` — 现实视频镜头检测结果
- `StoryboardShot` — 创作分镜镜头
- `StoryboardPanel` — 漫剧/分镜画面单元
- `TimelineClip` — 时间线上的编辑片段
- `ContentProject` — 内容业务项目
- `CreativeProject` — AI 创作项目
- `BroadcastSession` — 广播运行会话
- `ResearchExperiment` — 模型研究实验

最终命名以实际 Schema/API 交叉审计为准。

## 5. 资产血缘

```text
Source Asset
   ↓
Derived Artifact
   ↓
Analysis / Knowledge Artifact
   ↓
Dataset Sample
   ↓
Model Artifact
```

任何生成结果如果无法回答“由什么输入、哪个版本、哪个引擎产生”，都不应被视为生产级 Artifact。