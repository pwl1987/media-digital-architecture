# Portfolio Census — 2026-08-29

本文件记录本轮从 `pwl1987` GitHub 仓库列表中发现的、与媒体 / AI / 内容 / 创作 / 直播 / 数据存在潜在关系的项目。它的目的不是把所有仓库都纳入融合，而是避免遗漏历史技术路线。

## 纳入规则

只有满足以下至少一项才进入媒体数字智能考古范围：

- 内容管理、媒资、视频、直播、广播、AI 创作、AI 数据、模型训练、文化产品；
- 能产生或消费 Content / Asset / Artifact / Knowledge / Dataset / Model；
- 明显属于现有主线项目的前身、平行实现或实验实现。

## 第一梯队：直接影响目标架构

| Repo | 角色判断 | 当前处置 |
|---|---|---|
| news-media-system | Content / Business Control Plane | KEEP / CORE |
| YimengSpirit-Multimodal | Domain Intelligence | REBUILD / CORE |
| media-ai-platform | AI Video Production Platform | CONSOLIDATE |
| lamice | Creative Studio / Application | CONSOLIDATE |
| lamice-platform | Creative Platform implementation branch | CONSOLIDATE / EXTRACT |
| live-platform | Live Operations | KEEP / CORE |
| VBMF | Broadcast Media Fabric | KEEP / CORE |
| video-shot-detection | Shot Detection Engine | EXTRACT |
| video-compression-system | Compression / Quality Engine | EXTRACT |
| ai-spider-annotation | Data Studio | REBUILD / EXTRACT |
| yimengjingshen | Research / Model Lab | KEEP AS LAB |
| xiao-opera-miniapp | Consumer Experience | REBUILD / PRODUCT |
| media-platform | Legacy Business Platform | FREEZE / EXTRACT |
| city-converged-media-platform | Legacy Business Platform | FREEZE / EXTRACT |
| video-management-system | Legacy Video CMS | FREEZE / EXTRACT |
| YimengHeart | Legacy Yimeng Q&A | RETIRE / COMPATIBILITY |

## 第二梯队：需要继续考古，可能提供资产

### ai_story

定位是从主题到故事视频的自动化生产平台，包含文案、分镜、图片生成、运镜、视频生成、项目、提示词、模型配置、实时进度等；README 同时声明导演模式仍在开发。fileciteturn192file0L2-L2

判断：这是又一条 AI 视频生产路线，与 `media-ai-platform / LAMICE` 高度重叠。代码不应继续独立成为第四套 Creative Platform；重点抽取其工作流产品经验、导演模式 UX、提示词与生成阶段模型。

### waoowaoo-dev

定位和 `ai_story` 类似，仍是 Next.js 15 + React 19 + MySQL + Prisma + Redis/BullMQ，并明确声明处于测试初期；同时说明数据库版本之间可能不兼容，升级甚至要求清除卷。fileciteturn194file0L2-L2

判断：这是 Creative Platform 历史/实验路线的重要考古源，不应成为新的生产主线。

### openreel-video

这是一个第三方开源的浏览器视频编辑器范式，使用 React/TypeScript/WebCodecs/WebGPU、Zustand、IndexedDB，定位为全客户端编辑；README 宣称约 130k+ 行代码并处于 Beta。fileciteturn193file0L2-L2

判断：不属于 `pwl1987` 自有系统，不应纳入代码融合；可以作为 Creative Studio 的外部架构参考，尤其是浏览器端 Timeline、Undo/Redo、Artifact-local storage、WebCodecs/WebGPU 等设计。

### aigcpanel

AigcPanel 是一站式 AI 数字人桌面软件，重点是视频合成、TTS、声音克隆、模型导入和本地模型管理；其模型插件通过 `config.json + server.js` 定义能力，并通过进程/HTTP方式运行模型。fileciteturn198file0L2-L2

判断：它不是主业务系统，但其“Model Package / Runtime Adapter / capability discovery”思想值得进入统一 Model Contract / Runtime Contract 的考古对照；禁止直接复制成另一套 Provider Registry。

### media-source-extract

这是 `pwl1987` 对外部 `Momo707577045/media-source-extract` 的 fork，主题是 MediaSource 视频资源提取/下载，源仓库为外部项目。fileciteturn196file0L2-L2

判断：属于工具型 fork，不是媒体平台的核心资产；应归 `External Fork / Tooling`，不进入核心架构，也不作为内容采集主链。涉及采集时必须遵守授权、站点条款和版权要求。

## 第三梯队：暂不纳入融合主线，但保留索引

包括 `WebAV`、`QuickCut`、`CutClaw`、`openreel-video` 等具有媒体编辑/浏览器媒体能力的项目。它们可作为技术参考或局部实验，但除非后续审计证明存在高价值自有代码，否则不创建新的平台级依赖。

## 新增治理原则

### 1. 外部 Fork 不是自有架构资产

Fork 的代码必须记录上游来源、许可证、版本和修改范围。不得因为 fork 在个人 GitHub 账号下就当成内部原创平台能力。

### 2. 相同产品概念出现第三次时，默认不是“再建一个项目”

例如 Creative Video Production 已经出现多次实现。后续新增实现必须走 ADR，解释为什么现有 Creative Platform 无法承担。

### 3. “功能描述很完整”不能提高项目健康等级

必须由代码、运行、测试和真实闭环证据升级等级。

### 4. 外部项目只进入 Reference Catalog

外部项目可以影响技术选型，但不能成为内部 Source of Truth，除非完成许可证、供应链、API 稳定性与维护风险评估。
