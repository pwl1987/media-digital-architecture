# Archaeology — YimengSpirit-Multimodal

## 定位

沂蒙领域 AI / Intelligence Plane 候选核心，但当前仍属于“AI 工程骨架 + 部分可运行能力”阶段，不应把路线图完成度等同于产品完成度。

## 已确认的技术事实

- Python 3.12 限定，`pyproject.toml` 当前生产 extra 仍明确把 vLLM/FastAPI/FAISS 等列为后续填充项。fileciteturn142file0L2-L2
- 推理核心实际覆盖：纯文本、单图图文、多轮纯文本、多轮带当轮图，以及流式文本；当前多轮视觉语义是“历史图剥离、只保留当轮图”。fileciteturn138file0L2-L2
- 模型运行以 MiniCPM-V 为强假设，模型加载/推理/serving 仍是该仓库内部边界。

## 关键考古结论

### 1. 真实能力不等于“完整多模态平台”

当前最硬的代码证据是文本 + 单图 + 多轮文本/当轮图。视频、文档等更大范围能力仍属于规划/扩展，不应在产品层宣称为已经闭环。

### 2. 多轮视觉上下文存在有意损失

历史图片被剥离以控制显存，因此这是一个明确的产品语义约束，不是纯实现细节。后续必须在 API/UI 明示“视觉上下文保留策略”，避免用户以为模型记得全部历史图片。

### 3. Python 配置层仍偏“动态 wrapper”

`Config`/YAML/env 方案是工程骨架，不应成为全生态公共配置模型。最终应统一解析语义，而不是统一 YAML 文件。

### 4. 生产 Serving 尚未成为已验证主链

生产 extra 尚在建设，所以 vLLM/SGLang 等不能在当前阶段当作已验证生产基线。

### 5. 领域知识价值大于模型品牌

MiniCPM-V 是当前 runtime 选择，不应成为跨系统领域模型的事实源。需要把 Knowledge/Evidence/Dataset/Model Artifact 与具体模型解耦。

## 高价值资产

- MiniCPM-V 领域推理封装
- 多模态推理形状/模板经验
- SFT/LoRA training skeleton
- Yimeng domain dataset pipeline
- Knowledge/RAG 设计
- Golden evaluation 方向

## 需要重建的部分

- Production serving contract
- AIResult / Evidence contract
- Knowledge provenance
- model/artifact registry
- 真实 Golden Eval
- 视频/文档处理闭环

## 最终命运

**Rebuild/Continue**

这是值得投资的核心项目，但不应按当前结构无限加功能。未来目标是“Intelligence Plane”，不拥有企业用户、CMS、全局导航或第二套 AI governance。

## 迁移优先级

P0：AIResult / Evidence / Model Artifact / Knowledge Contract

P0：Golden Eval

P1：Serving abstraction 与实际 production runtime

P1：与 `news-media-system` 的 MediaAsset/Artifact 接口

P2：视频/文档多模态闭环
