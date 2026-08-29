# Repository Portfolio Register

> 初始族谱扫描；此表用于区分“属于生态的项目”与“仅相关/外部参考项目”。

| Repository | Relation | Initial role | Disposition | Confidence |
|---|---|---|---|---|
| `news-media-system` | 核心 | Content/Business Platform | KEEP + HARDEN | high |
| `YimengSpirit-Multimodal` | 核心 | Intelligence | REBUILD/CONTINUE | high |
| `media-ai-platform` | 核心 | Creative Platform | CONSOLIDATE | high |
| `lamice` | 核心 | Creative Studio generation | EXTRACT | high |
| `lamice-platform` | 核心 | Creative Platform alternate generation | SELECTIVE REUSE / REBUILD | high |
| `live-platform` | 核心 | Live Operations | KEEP + ALIGN | high |
| `VBMF` | 核心 | Broadcast Fabric | PROTECT + IMPLEMENT | high |
| `video-shot-detection` | 核心能力 | Shot Engine | EXTRACT | high |
| `video-compression-system` | 核心能力 | Compression/QC Engine | EXTRACT / REBUILD SMALL | high |
| `ai-spider-annotation` | 核心能力 | Data Studio | REBUILD | high |
| `yimengjingshen` | 核心能力 | Research Lab | KEEP AS RESEARCH | high |
| `xiao-opera-miniapp` | 核心产品端 | Consumer Experience | REBUILD EXPERIENCE | high |
| `media-platform` | 历史 | Early Content Platform | FREEZE + EXTRACT | high |
| `city-converged-media-platform` | 历史 | Earlier Content Platform | FREEZE + EXTRACT | medium |
| `video-management-system` | 历史 | Earlier Video Platform | FREEZE + EXTRACT | medium |
| `YimengHeart` | 历史 | Legacy AI Chat | RETIRE / COMPATIBILITY | high |
| `ai_story` | 历史/参考 | AI story-video workflow | EXTRACT IDEAS | medium |
| `waoowaoo-dev` | 参考/衍生 | AI video studio lineage | REFERENCE / EXTRACT IDEAS | medium |
| `aigcpanel` | 参考 | local AI model runtime packaging | REFERENCE | medium |
| `WebAV` | 参考/候选能力 | browser media processing | EVALUATE | medium |
| `QuickCut` | 参考/候选能力 | editing/cutting UX | EVALUATE | low |
| `CutClaw` | 参考/候选能力 | AI-assisted media editing | EVALUATE | low |
| `openreel-video` | 外部参考 | browser video editor | EXTERNAL REFERENCE ONLY | high |
| `media-source-extract` | 外部 fork | browser MediaSource extraction reference | EXTERNAL/FORK; NO CORE OWNERSHIP | high |
| `CCTVVideoDownloader` | 相关工具 | media acquisition | OUTSIDE CORE ARCHITECTURE FOR NOW | medium |
| `flow-kit` | 相关资产 | media/AI workflow material | INVESTIGATE | medium |
| `rm-contest-writer` | 相关内容工具 | writing/content production | INVESTIGATE | low |
| `openreel-video` | 外部项目 | browser editor benchmark | EXTERNAL REFERENCE ONLY | high |

## Classification rules

### Core

直接影响目标平台产品、业务或关键基础设施。

### Core capability

不应成为独立业务平台，但有明确可复用技术能力。

### Historical

以前的实现、实验或旧产品，不作为未来架构 owner。

### Reference

有借鉴价值，但不应被误认为是自有生产资产。

### External/Fork

代码来源或产权归属需单独确认；不能默认纳入自有产品资产。

## Important findings

1. `media-source-extract` 是对外部 `Momo707577045/media-source-extract` 的 fork，必须作为 external/fork reference 处理，而不是自有核心资产。
2. `ai_story`、`waoowaoo-dev`、`media-ai-platform`、`lamice`、`lamice-platform` 已形成一条明显的 AI 视频创作重复谱系，需要统一领域后择优重建。
3. `aigcpanel` 的“模型目录 + runtime adapter + 标准输出”思路值得用于 Model Runtime Contract 设计，但不应直接复制其产品边界。
4. `openreel-video` 是外部项目，只可作为浏览器编辑器能力 benchmark，不应进入自有代码血统。

## Audit status

本表不是最终处置清单。任何 `medium/low` confidence 项必须继续 code-level archaeology 后才能升级为最终决策。