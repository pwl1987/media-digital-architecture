# Archaeology — media-platform

## 定位

旧一代融媒体后端骨架。README 明确称其为依据设计规范搭建的“最小可运行骨架”，覆盖 13 个模型、首次迁移、MinIO、Celery、SQLAdmin、种子、Docker 和验收脚本。fileciteturn168file0L2-L2

## 高价值资产

- FastAPI 分层组织。
- Pydantic API schema。
- SQLAlchemy/Alembic 迁移。
- S3/MinIO storage abstraction。
- Celery cpu/io/video/gpu 队列模型。
- health/ready、request id、错误码、响应 envelope。
- 对 SQLite 与真实 PostgreSQL 差异的工程经验。

## 主要问题

1. 已经与 `news-media-system` 形成平台级重复。
2. Celery + Redis + FastAPI 与当前 Business baseline 不一致。
3. 作为“最小骨架”完成了基础设施，但没有形成与现有新平台相比明显不可替代的业务优势。
4. 继续开发会制造第二套 Content/Media/Job/Storage 世界。

## 最终命运

**Freeze / Extract**

不恢复成第二融媒体平台。抽取：

- storage abstraction
- health/ready pattern
- error/response contract 思路
- Celery worker 经验
- 迁移/验收脚本经验

业务数据模型不直接成为新系统 canonical schema。
