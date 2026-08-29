# Source of Truth Policy — Draft 0.1

## 1. 目标

避免多个仓库通过 README、计划文档、数据库、代码和共享类型分别定义“事实”，最终导致无法判断哪个版本正确。

## 2. Truth hierarchy

### L0 — Runtime behavior

实际生产代码、数据库 migration、协议实现是行为事实；文档不能与运行时相矛盾。

### L1 — Data schema

Canonical object schema、数据库 migration、JSON Schema 是数据结构事实。

### L2 — API / Event contracts

OpenAPI / AsyncAPI / JSON Schema 是跨系统接口事实。

### L3 — Architecture ADR

本仓库的 ADR 记录架构决策、边界、禁止事项和迁移选择。

### L4 — Product specification

产品规格定义用户价值和业务行为，不定义底层实现细节。

### Non-authoritative

计划、任务单、AI 生成说明、临时报告、review notes 仅是过程材料，不能成为长期事实源。

## 3. Shared package policy

`news-media-system` 已有 `@news-media/shared` 和 `@news-media/ui`。这些可以继续服务其业务单体/前端生态，但不得自动升级为整个多仓库生态的公共事实源；跨系统 contract 必须进入独立版本化的 contracts 目录。

## 4. Database policy

一个系统可以拥有自己的数据库 schema，但任何跨系统共享的数据必须拥有明确 owner。禁止通过“直接查询别人的数据库”绕过 API/Event Contract。

## 5. API policy

业务系统不得把内部 ORM schema 直接作为公共 API。DTO/JSON Schema 才是公共契约。

## 6. Change control

任何新增一级对象、跨系统 API、事件类型、存储语义或控制面能力，必须先在 `media-digital-architecture` 建立决策记录，再进入实现仓库。
