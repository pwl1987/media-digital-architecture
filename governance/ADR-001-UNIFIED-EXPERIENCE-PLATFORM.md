# ADR-001 — Unified Experience Platform

- Status: Proposed
- Date: 2026-08-29
- Scope: ecosystem-wide

## Decision

建立一个统一的主题主平台（暂名 `media-digital-platform`）作为 Experience / Identity / Navigation / Workspace / Cross-system Orchestration 层。

它不取代专业业务系统，不拥有各专业域的核心业务事实。

## Responsibilities

- SSO / identity handoff
- organization and role context
- global navigation
- workspace switching
- global search entry
- global task center
- notification entry
- module registry
- health/version visibility
- cross-system deep links
- unified design shell

## Explicitly out of scope

- CMS content source of truth
- media bytes processing
- model runtime
- broadcast device control
- creative rendering internals
- research experiment execution

## Architecture

```text
                     media-digital-platform
                               │
             ┌─────────────────┼─────────────────┐
             ▼                 ▼                 ▼
       Content Module      AI Module       Creative Module
             │                 │                 │
             ▼                 ▼                 ▼
       news-media-system   Yimeng AI       Creative Platform

             ┌─────────────────┼─────────────────┐
             ▼                 ▼                 ▼
        Live Module      Broadcast Module    Knowledge Module
             │                 │                 │
             ▼                 ▼                 ▼
       live-platform          VBMF            Yimeng AI
```

## Rationale

当前项目群存在多个独立 UI、身份入口、菜单和工作流。通过主题 Shell 统一用户体验，比把所有仓库合并成一个 Monolith 更符合专业系统的生命周期。

## Migration

1. 先定义 module manifest。
2. 先统一身份、导航、Design Tokens、任务语义。
3. 以 News / AI / Creative 三个代表页面验证 Shell。
4. 再接入 Live / Knowledge / Broadcast。
5. 最后考虑更深的前端集成；不以微前端为第一阶段前提。

## Consequence

专业系统可以继续独立部署；用户看到的是一个产品家族。跨系统集成必须使用 API/Event/SSO Contract，不直接共享数据库。
