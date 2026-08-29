# Archaeology — Creative Family

本档案联合记录 `media-ai-platform`、`lamice`、`lamice-platform` 三条 Creative/LAMICE 技术路线。

## 1. 结论先行

这是目前整个生态最明显的“重复建设 + 多代迁移未收口”区域。

```text
waoowaoo / media-ai-platform
        ↓
lamice / Next.js + Prisma + BullMQ
        ↓
lamice-platform / FastAPI + SQLAlchemy + Vue3
```

三套体系都在定义 project / episode / character / location / storyboard / task / provider / billing / generation 等概念。

## 2. media-ai-platform

README/代码事实：Next.js 15 + React 19 + MySQL + Prisma + Redis/BullMQ + Remotion；package scripts 同时包含 Next server、worker、watchdog、Bull Board，并存在 provider/capability/task/coverage/行为回归等大量 guard。fileciteturn173file0L2-L2 fileciteturn134file0L2-L2

### 价值

- 已投入大量业务/工程治理。
- AI provider/capability、task、billing、media normalization、outbound media 等有较强工程资产。
- 适合提炼 Creative orchestration 思想和 guard/test 资产。

### 问题

- 产品、平台、provider、runtime 责任高度耦合。
- 与 `lamice` 功能/技术栈高度重叠。
- 数据模型出现 imageUrl/imageUrls 与 MediaObject 并存的历史演化迹象；需要以 Artifact/Media identity 重构。fileciteturn139file0L2-L2
- README 仍明确是测试初期 beta，不能把大量 guard 数量等同于产品完成度。fileciteturn173file0L2-L2

### 建议

**Consolidate → Creative Platform Core**

保留运行时和成熟业务逻辑，但必须与 Studio UI 分离。

## 3. lamice

README 明确主链：剧本分析、角色/场景、分镜、视频、配音；同时明确 CapCut 导出和合规审核属于实验性能力，不能作为生产闸门。fileciteturn174file0L2-L2

### 价值

- 产品心智比纯 backend 更清晰。
- 已有真实创作主链。
- React/Next 体验适合作为 Creative Studio 参考。

### 问题

- 仍与 media-ai-platform 共享同一技术基因。
- README 中 Docker/目录示例有明显历史遗留命名（仓库叫 lamice，但命令仍出现 waoowaoo-custom），说明文档/产品迁移未完全清理。fileciteturn174file0L2-L2

### 建议

**Studio-first**：保留用户创作体验；后端能力逐步转移至最终选定的 Creative Platform。

## 4. lamice-platform

这是最特殊的一条路线。README 自称基于 FastapiAdmin 插件式架构，FastAPI + SQLAlchemy + Alembic + Vue3/ElementPlus，声明 312 tests / 91% coverage；同时明确列出关键未完成：Storage 路由未注册、项目/剧集缺 status、编辑器只是 CRUD 骨架、Prompt 管理缺失等。fileciteturn175file0L2-L2

### 判断

它不是“更完整的 LAMICE”，而是“高工程化但未完成的第三代平台重构候选”。

### 价值

- 插件边界思想不错。
- 后端竖切模块化值得提取。
- 测试/coverage/迁移/模块化治理经验可复用。

### 问题

- 又引入 Vue3/ElementPlus + FastAPI/SQLAlchemy，与既有主业务基线不一致。
- 支持 MySQL/PostgreSQL/SQLite 三种数据库，增加运行矩阵。
- 工作流仍标“骨架”，编辑器也是骨架，因此不能用测试数量掩盖业务未闭环。fileciteturn175file0L2-L2

### 建议

**Selective extraction / Rebuild**。

不建议把它作为第四个长期平台。优先提取：

- 模块化组织方式
- Workflow/Step registry
- billing ledger 思想
- SSE execution progress
- 测试与质量门禁

生产数据库/前端主技术栈应向生态基线收敛。

## 5. 最终目标

```text
Creative Platform Core
├── CreativeProject
├── Episode
├── Character
├── Location
├── Storyboard
├── Generation
├── Job
├── Artifact
├── Billing/Usage
├── Timeline/Render
└── Provider orchestration
           ↑
      LAMICE Studio
```

三代代码不应三线并存。必须在母架构库中选择一套 canonical object + 一条 production runtime 主线。
