# ADR-004 — AI Intelligence Boundary

- Status: PROPOSED
- Date: 2026-08-29

## Decision

把 AI 体系拆成三个语义层：

```text
Business Capability
        ↓
AI Orchestration / Intelligence Service
        ↓
Model Runtime / Provider
```

### Business Capability

描述业务要完成什么：

- article.summary
- article.rewrite
- media.analyze
- media.transcribe
- media.ocr
- knowledge.search
- knowledge.answer
- creative.generate
- media.shot_detection

业务请求不得绑定具体模型名称。

### Intelligence Service

负责：

- prompt/agent orchestration
- retrieval
- evidence grounding
- model selection input
- request normalization
- result normalization
- evaluation
- provenance

`YimengSpirit-Multimodal` 是领域 Intelligence 的主要实现候选。

### Model Runtime / Provider

负责实际执行：

- local transformers
- vLLM / SGLang
- Alibaba
- Volcano
- other OpenAI-compatible providers

Runtime-specific configuration 不得泄露进业务 contract。

## Existing evidence

`news-media-system` 当前已经有 AI capability、provider、model/config 和 adapter 抽象；因此不应再在每一个 AI 产品内复制一套业务级 provider registry。

`YimengSpirit-Multimodal` 当前可以直接执行 MiniCPM-V inference，但其生产边界应定义成 Intelligence/Data Plane，而不是第二个企业业务 AI Governance Plane。

## OpenAI compatibility

OpenAI-compatible API 可以作为底层 model serving interface；它不是整个业务 AI API 的最终契约。

上层应优先调用业务语义接口，再由 orchestration 映射到 model API。

## Result contract

AI 结果不应只有 `content`。生产级结果应至少支持：

- result/content
- model reference
- generation reference
- evidence references
- source references
- usage
- trace id
- policy/check result
- output artifact references

## Safety / trust

历史文化类 AI 必须支持：

- evidence-first retrieval
- source authority
- uncertainty
- conflict detection
- abstention
- provenance

“模型输出了答案”不等于“事实得到确认”。
