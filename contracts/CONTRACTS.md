# Cross-System Contracts — Draft 0.1

## 1. Contract Philosophy

跨仓库集成首先依赖语义契约，而不是共享内部代码。

原则：

- API Contract 定义请求/响应语义。
- Job Contract 定义异步计算生命周期。
- Event Contract 定义事实发生后的通知。
- Artifact Contract 定义结果产物。
- Storage Contract 定义对象访问抽象。
- AI Capability Contract 定义“能力”而不是绑定某个模型 Provider。
- Model Contract 定义模型身份、版本、能力和运行状态。

## 2. Job Contract

建议统一最小语义：

```json
{
  "job_id": "J-...",
  "type": "media.shot_detection",
  "status": "queued",
  "progress": 0,
  "input_artifacts": [],
  "output_artifacts": [],
  "producer": "shot-engine",
  "producer_version": "...",
  "error": null,
  "created_at": "...",
  "updated_at": "..."
}
```

允许不同运行时：BullMQ、Celery、专用实时 runtime 等。统一语义，不强制统一 Queue 技术。

## 3. Event Contract

事件应描述“已经发生的事实”，而不是 RPC 命令。

初始事件命名建议：

- `media.asset.created`
- `media.asset.updated`
- `media.artifact.created`
- `media.processing.started`
- `media.processing.completed`
- `media.processing.failed`
- `media.shot.detected`
- `ai.job.started`
- `ai.job.completed`
- `ai.job.failed`
- `knowledge.updated`
- `video.render.completed`
- `broadcast.session.started`
- `broadcast.session.health_changed`
- `broadcast.session.switched`

事件 schema 后续单独冻结。

## 4. API Contract

跨系统 API 必须：

- 使用稳定 resource identity。
- 不暴露底层数据库 schema 作为公共契约。
- 不要求消费者知道实现技术。
- 明确状态机和错误模型。
- 支持幂等键（涉及创建/提交操作时）。
- 明确版本策略。

## 5. Storage Contract

业务系统不直接假定某个具体对象存储厂商。

```text
Artifact
  ↓
Storage abstraction
  ↓
S3 / RustFS / MinIO / NAS / other provider
```

URI、bucket、path 都属于 locator；Artifact ID 才是业务身份。

## 6. AI Capability Contract

上层请求：

```text
capability = vision.image_understanding
capability = text.generation
capability = speech.to_text
capability = media.shot_detection
capability = image.generation
capability = video.generation
```

不要直接在业务 API 中硬编码具体模型名，例如把 `qwen-xxx`、`model-a` 当作业务能力。

Provider/Model 是 Capability 的实现。

## 7. Broadcast / Live Contract

实时媒体系统采用专用 Session/Channel/Health/Switch 语义，不强制套用普通 Job Contract。

- Live Operations 面向 stream/session/channel。
- VBMF 面向 broadcast source/fabric/health/switch/redundancy。
- 业务平台只依赖控制 API。

## 8. Versioning

跨系统契约必须可版本化。

建议：

```text
contract name + major version
```

破坏性变更升级 major；兼容扩展不应无意义地复制新对象。

最终 OpenAPI / JSON Schema / AsyncAPI 文件将在后续审计阶段加入本仓库。