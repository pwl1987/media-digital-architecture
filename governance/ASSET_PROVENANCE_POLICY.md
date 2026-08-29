# Asset Provenance Policy

## Why

项目群中同时存在自研仓库、历史仓库、fork、第三方参考项目、模板和衍生项目。必须先判断 provenance，再谈复用与迁移。

## Provenance classes

| Class | Meaning | Allowed action |
|---|---|---|
| OWNED | 自研且拥有代码/数据使用权 | 可评估迁移/重构 |
| DERIVED | 基于自有项目演进或重构 | 需记录血统关系 |
| FORK | 对外部仓库 fork | 不得默认视为原创资产 |
| EXTERNAL | 第三方项目 | 只可作为参考，需遵守许可 |
| UNCERTAIN | 来源尚未确认 | 禁止进入生产迁移，先核实 |

## Required provenance record

每一项拟迁移资产至少记录：

```yaml
provenance:
  repository:
  path:
  origin_class:
  upstream:
  license:
  ownership_confirmed: false
  notes:
```

## Rules

1. Fork 不等于原创；需要记录 upstream。
2. 第三方项目可以影响技术选型，但不得直接复制进核心平台而不确认许可证和来源。
3. 仅因为仓库出现在同一 GitHub 用户下，不代表它属于同一产品血统。
4. 外部参考只能进入 architecture benchmark，不自动进入 migration map。
5. 未确认 provenance 的代码进入 UNCERTAIN 状态，不得作为生产依赖。

## Current examples

- `pwl1987/media-source-extract`：GitHub metadata 表明其 parent/source 是 `Momo707577045/media-source-extract`，因此按 FORK / EXTERNAL reference 处理。
- `openreel-video`：外部开源项目，只作为浏览器编辑器 benchmark。
- `aigcpanel`：外部/参考代码可以启发 Model Runtime Contract，但不进入核心代码血统。

## Relation to archaeology

考古报告需要把：

```text
Code value
Domain value
UX value
Research value
```

与 provenance 分开评价。

一个外部项目可以“技术价值很高”，但仍然不能因此变成“自有代码资产”。