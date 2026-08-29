# Archaeology — Intelligence, Data and Research

## YimengSpirit-Multimodal

Role: **Intelligence Plane candidate**.

The repository is aimed at multimodal domain intelligence: LLM/VLM, RAG/knowledge, multimodal processing, model serving and domain-oriented AI. Its future value is high, but the implementation should be rebuilt around platform-wide contracts instead of accumulating a second business platform.

### Keep
- multimodal inference pipelines
- knowledge/RAG processing
- model/runtime adapters
- domain-specific evaluation and grounding concepts

### Do not own
- enterprise identity
- CMS content truth
- global billing/quota policy
- consumer user system
- media storage identity

## ai-spider-annotation

Role: **Data Studio candidate**.

The README explicitly still marks data model, crawler, annotation, AI export, performance, testing and documentation as unfinished. This is strong evidence that the project is a prototype/partial implementation rather than a completed platform.

Target flow:

```text
Ingest → Normalize → Annotate → Review → DatasetSample / KnowledgeArtifact
```

The valuable asset is the annotation workflow and data transformation idea. The project should not retain an independent production identity/storage universe.

## yimengjingshen

Role: **Research Lab**.

The source project lineage is explicitly about building and training small language models and includes pretraining, SFT, LoRA, DPO, RLAIF, tool use, agentic RL, evaluation and serving. Its correct output boundary is ResearchExperiment and ModelArtifact, not a production business service.

## Intelligence boundary

```text
Business Capability / Policy
        ↓
Intelligence API
        ↓
Yimeng Intelligence
        ↓
Model Runtime
```

Research must produce versioned artifacts. Production services consume registered model artifacts rather than importing research code directly.

## Evidence policy

Claims such as “multimodal platform”, “complete data pipeline”, or “full training chain” must be recorded separately from verified runtime completion. A README feature list is E0 unless implementation and runtime evidence are found.
