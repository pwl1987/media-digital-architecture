# Portfolio Lineage

> 当前媒体/AI项目群的演进血统与重启模式

## Content / CMS lineage

```text
media-platform
      ↓
city-converged-media-platform
      ↓
news-media-system
```

### Archaeological interpretation

这条线反复解决的是“融媒体业务平台”问题。后续原则是不再创建第四套 Content Platform。`news-media-system` 作为当前主线，旧项目只贡献经过验证的模式、迁移数据和少量可复用代码。

## Creative / AI video lineage

```text
ai_story
      ↓
waoowaoo-derived work
      ↓
media-ai-platform
      ↓
lamice
      ↓
lamice-platform
```

### Archaeological interpretation

这一条线反复出现 Script / Storyboard / Character / Scene / Generation / Task / Worker / Provider 等相同概念，但多次更换实现栈。这是当前最典型的“架构重启”案例。

目标不是选择“代码最多”的一代，而是抽取稳定领域模型和可靠运行能力，重建一个 Creative Platform Core；LAMICE 作为 Studio/Application 层。

## Yimeng Intelligence lineage

```text
YimengHeart
      ↓
yimengjingshen
      ↓
YimengSpirit-Multimodal
```

### Archaeological interpretation

演进方向由聊天应用 → 模型研究 → 领域多模态智能。生产系统应承接领域知识、模型 artifact、评测和推理能力，不继承旧聊天应用的业务边界。

## Media processing lineage

```text
video-management-system
      ↓
video-shot-detection
      ↓
video-compression-system
      ↓
news-media-system / Media Processing integration
```

### Archaeological interpretation

“视频系统”逐渐拆成多个专业引擎更合理。Shot、Compression、Transcode、QC 等应作为处理能力，不再各自演化成新的业务平台。

## Live / Broadcast lineage

```text
live-platform
      ↘
       media runtime ecosystem
      ↗
VBMF
```

### Archaeological interpretation

二者不是同一产品：live-platform 是 Live Operations，VBMF 是 Broadcast Runtime/Fabric。应通过控制与运行时契约协作。

## Data / Research lineage

```text
ai-spider-annotation → Data Studio

yimengjingshen → Research Lab → Model / Dataset Artifacts
```

## Consumer lineage

```text
xiao-opera-miniapp
      ↓
Yimeng Culture / Consumer Experience
```

## Key historical pattern

```text
问题出现
  ↓
新项目重建
  ↓
部分能力完成
  ↓
架构/体验不满意
  ↓
再次重建
```

母架构的核心作用就是在下一次重建前强制回答：

- 是否已有 canonical owner？
- 哪些能力已经存在？
- 哪些代码真正验证过？
- 哪些只是设计/计划？
- 新 Runtime 是否必要？
- 新项目与旧项目的边界是什么？

**原则：禁止因为“不舒服”而默认重启；必须先考古、量化、取舍。**