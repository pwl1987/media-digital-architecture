# Recovery-First Portfolio Roadmap — Draft 0.1

## 1. Principle

现有仓库普遍存在未完成、半成品、重复建设和历史技术债。当前阶段不以“把旧项目全部救活”为目标，而以建立新的 Canonical platform，并有选择地吸收高价值资产为目标。

## 2. Four questions before any rewrite

对每个旧仓库先回答：

1. 业务价值：现在是否有真实用户/真实业务？
2. 领域价值：现有模型是否值得保留？
3. 技术价值：哪些代码已经可靠到值得迁移？
4. 迁移价值：保留/迁移是否比重写更便宜？

## 3. Decision matrix

```text
High business + high technical value
→ Recover / continue

High business + low technical value
→ Rebuild on canonical architecture

Low business + high technical value
→ Extract engine / algorithm / contract

Low business + low technical value
→ Freeze / retire
```

## 4. Current first-wave actions

### Wave A — protect the new core

- Keep `news-media-system` as Business Control Plane candidate.
- Keep `YimengSpirit-Multimodal` focused on Intelligence capabilities, but stop uncontrolled platform expansion.
- Keep `VBMF` isolated as Broadcast Runtime/Fabric.

### Wave B — stop duplication

- `media-platform`: no new feature unless migration-critical.
- `YimengHeart`: compatibility only.
- `media-ai-platform` + `LAMICE`: freeze new duplicate infrastructure while Creative architecture is consolidated.

### Wave C — extract engines

- `video-shot-detection`: define `ShotDetection` contract and promote engine.
- `video-compression-system`: define `MediaProcessing`/quality contract and promote engine.
- Future ASR/OCR/transcode services follow same engine rules.

### Wave D — data

- `ai-spider-annotation`: become Data Studio against Dataset/Annotation contracts.
- `yimengjingshen`: remain Research Lab; export Dataset/Model/Evaluation artifacts through contract.

### Wave E — experience

- Create the theme shell only after the shared identity, navigation, task and design contracts are defined.
- `xiao-opera-miniapp` consumes the same business/intelligence APIs; it does not become another backend source of truth.

## 5. Recovery gate

一个旧系统只有通过以下 Gate 才能重新进入 feature development：

```text
G0 Inventory complete
G1 Critical flow identified
G2 Dependencies understood
G3 Canonical owner assigned
G4 Test/smoke baseline exists
G5 Production value confirmed
G6 Migration boundary documented
```

未过 G0-G3 的项目禁止继续扩大功能面。

## 6. Portfolio success criteria

最终评价不是“多少旧项目被救活”，而是：

- 新平台是否减少重复能力
- 用户是否获得连续一致的体验
- 内容/媒体资产是否可追踪
- AI 结果是否可验证
- 专业运行时是否保持隔离
- 旧项目是否得到明确命运
- 新功能是否只出现一个 Canonical owner
