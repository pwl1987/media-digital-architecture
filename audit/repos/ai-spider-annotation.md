# Archaeology — ai-spider-annotation

## 定位

典型的数据采集/标注半成品，应作为 `Data Studio` 重建来源，而不是继续独立发展平台。

README 当前技术栈是 FastAPI + Scrapy + SQLite，前端 Vue3 + Element Plus + Vite；开发计划仍把“数据模型、爬虫、标注、AI 导出、性能优化、测试文档”列为未完成。fileciteturn179file0L2-L2

## 可复用资产

- Scrapy 数据采集思路。
- 标注任务/预标注方向。
- JSON/CSV/HuggingFace 数据导出思路。
- Data Studio 的交互需求。

## 主要问题

1. SQLite 不适合作为生态级数据资产的唯一事实源。
2. 项目 README 的“智能爬虫/多种标注”更多属于目标能力，不能视为已完成闭环。
3. Vue3/ElementPlus 与企业 Web 新基线不一致。
4. 采集、清洗、标注、导出与知识库/训练集之间没有统一 Dataset/Artifact lineage。

## 最终命运

**Rebuild as Data Studio**

保留算法、交互和需求经验；重建数据模型、权限、Job、Artifact、DatasetVersion，并通过统一契约接入 Yimeng Intelligence。

## 目标链路

```text
Source
 ↓
Raw Asset
 ↓
Cleaning
 ↓
Annotation Task
 ↓
Review
 ↓
DatasetVersion
 ├── Knowledge
 └── Training/Eval
```
