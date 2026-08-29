# Recovery Decision Matrix — Draft 0.2

> 该矩阵用于防止“烂尾项目=继续补功能”的惯性。

| Repo | 主要价值 | 当前状态 | 主要缺口 | 决策 |
|---|---|---|---|---|
| news-media-system | 内容/媒资业务事实源、Business Control | 相对成熟但复杂 | 跨系统契约、部署语义、逐页 UX | **RECOVER + CORE** |
| YimengSpirit-Multimodal | 沂蒙 AI / Knowledge / VLM | 可运行骨架，产品未闭环 | production serving、Evidence、Eval、Knowledge lineage | **REBUILD/CONTINUE** |
| media-ai-platform | Creative orchestration、provider/task/billing 工程资产 | 重型 beta / 与其他代重复 | 与 LAMICE 争夺同一域 | **CONSOLIDATE** |
| lamice | Creative Studio 产品体验、主流程 | 有真实主链但仍有实验性能力 | 后端与平台职责 | **CONSOLIDATE AS STUDIO** |
| lamice-platform | 插件化后端、workflow、billing、测试经验 | 关键业务仍有骨架/缺口 | 与生态基线分叉 | **SELECTIVE EXTRACTION / REBUILD** |
| live-platform | ZLM、直播运营、监控、安全 | 可保留 | 技术栈落后、统一契约接入 | **RECOVER + ALIGN** |
| VBMF | 广播实时语义、Health、Switch、Fault Injection | 规范成熟，执行阶段 | Runtime implementation | **PROTECT + IMPLEMENT** |
| video-shot-detection | Shot detection algorithm | 专业 Engine | 标准 Job/Artifact 接口 | **EXTRACT** |
| video-compression-system | FFmpeg + quality gate | 小型工程骨架 | 完整 product/contract 证据不足 | **EXTRACT / FREEZE** |
| ai-spider-annotation | 数据采集/标注 | 明确未完成项 | 数据模型、主平台、权限、lineage | **REBUILD AS DATA STUDIO** |
| yimengjingshen | Research / training | 研究路线完整 | 不应生产化为业务平台 | **LAB / PRESERVE** |
| xiao-opera-miniapp | Consumer cultural UX | 产品壳有价值 | 后端、AI、身份、数据闭环 | **REBUILD AS CONSUMER** |
| media-platform | 旧 FastAPI/Celery/MinIO 骨架 | 旧平台 | 与 news-media 重复 | **FREEZE / EXTRACT** |
| city-converged-media-platform | 早期政务融媒体方案 | 声明大于证据 | 多域耦合、技术偏离 | **FREEZE / EXTRACT** |
| video-management-system | 早期视频全栈原型 | 典型功能堆叠 | 生产证据、领域分层 | **FREEZE / EXTRACT** |
| YimengHeart | 第一代问答 | legacy | 与新 AI 重复 | **RETIRE / COMPATIBILITY** |

## 决策规则

- **Recover**：核心业务价值高，代码与运行链有足够真实资产。
- **Rebuild**：业务价值高，但现有实现/边界不足以支撑未来架构。
- **Consolidate**：多个仓库争夺同一能力域，只保留一条 production 主线。
- **Extract**：保留算法/协议/测试/经验，不保留产品壳。
- **Freeze**：停止扩张，允许必要安全修复与迁移工作。
- **Retire**：仅保留兼容或历史资料。

## 重要结论

当前真正应该继续投资的不是所有仓库，而是：

1. `news-media-system`
2. `YimengSpirit-Multimodal`
3. `VBMF`
4. `live-platform`
5. 最终收敛后的 Creative Platform

其余项目多数应该为这五个核心提供资产、引擎、研究或体验，而不是继续形成自己的“完整平台”。