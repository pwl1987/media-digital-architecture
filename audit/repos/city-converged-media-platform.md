# Archaeology — city-converged-media-platform

## 定位

另一条早期“政务级融媒体平台”路线，功能目标覆盖媒体接入、AI处理、多平台分发、监控运维、安全合规；但与当前 `news-media-system` 的职责高度重叠。README 的技术路线是 Python3.13/FastAPI/SQLAlchemy/Alembic + SQLite→PostgreSQL，SRS6 + FFmpeg7，ONNX Runtime，本地 AI，Vue3/ElementPlus。fileciteturn180file0L2-L2

## 主要考古发现

1. **架构声明大于实现证据**：README 同时给出“等保三级”“100路并发”“100万素材”等目标指标，但这些属于目标，不应视为已验证生产能力。fileciteturn180file0L2-L2
2. **技术栈已经明显偏离当前基线**：FastAPI/SQLAlchemy/Vue/ElementPlus/SRS 与当前 Business/Live 分层并不一致。
3. **数据层仍存在 SQLite → PostgreSQL 的双环境语义**，与其他历史平台相似。
4. **内容、素材、直播、AI、监控被做成一体化“平台”，容易重复造轮子**。

## 高价值资产

- 政务级安全/审计需求表达。
- SRS/FFmpeg integration 经验。
- 内容分发、多源接入、监控运维产品需求。
- 可能存在的 API/database design 可作为旧方案对照。

## 最终命运

**Freeze / Extract**

不作为新的主平台恢复。提取安全要求、SRS 集成、运维经验和真正可验证的业务规则；统一迁入母架构对应层。

## 不应继承

- 其独立用户/权限/内容 schema。
- 其前端组件体系。
- 其 SQLite-first 业务语义。
- “一体化平台”导致的跨域耦合。
