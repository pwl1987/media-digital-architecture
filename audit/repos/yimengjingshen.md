# Archaeology — yimengjingshen

## 定位

**Model Research Lab**。它本质是 MiniMind/MiniMind 系列的从零训练与研究型项目，而不是沂蒙领域生产 AI 平台。README 明确覆盖 Pretrain、SFT、LoRA、DPO、PPO/GRPO、Tool Use、Agentic RL、蒸馏、评测和 OpenAI API 等完整研究链路。fileciteturn176file0L2-L2

## 高价值资产

- 从零实现 Transformer/训练核心的研究代码。
- Pretrain/SFT/LoRA/RL/Agentic RL 实验方法。
- Dataset、训练脚本、评测方法。
- 与 vLLM/llama.cpp/Ollama 等推理生态对接的经验。

## 不适合承担

- 企业用户与权限。
- 新闻内容业务。
- 正式知识库治理。
- 生产 AI provider/control plane。
- 领域业务 API。

## 主要风险

1. 研究仓库能力非常丰富，容易诱导“把实验代码直接搬进生产”。
2. 训练范式更新快，不宜成为生产服务的直接源码依赖。
3. 数据/模型产物应该通过 Model Artifact / Dataset Contract 输出，而不是跨仓库 import 内部模块。

## 最终命运

**Lab / Preserve**

保持独立。重点建设统一的：

```text
DatasetVersion
TrainingRun
ModelArtifact
EvaluationReport
```

生产侧只消费不可变 Artifact。
