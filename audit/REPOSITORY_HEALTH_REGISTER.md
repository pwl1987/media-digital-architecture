# Repository Health Register — Draft 0.1

本登记表用于持续记录各仓库的“事实状态”。它把“项目存在”“项目活跃”“项目可用”“项目完成”分开。

## 1. Status dimensions

| Dimension | Values |
|---|---|
| Lifecycle | proposed / active / consolidating / frozen / legacy / retired |
| Health | green / yellow / orange / red |
| Functional state | complete / partial / prototype / mock / broken / unknown |
| Runtime state | production / staging / dev-only / cannot-start / unknown |
| Evidence level | proven / partially-proven / documentary-only |

## 2. Current register

| Repository | Lifecycle | Health | Functional state | Runtime | Evidence | Current disposition |
|---|---|---|---|---|---|---|
| `news-media-system` | active | yellow* | partial/active | production-capable* | proven/partial | Core; recover and simplify |
| `YimengSpirit-Multimodal` | consolidating | orange* | prototype/partial | dev/research* | partial | Rebuild selectively as Intelligence Core |
| `media-ai-platform` | consolidating | orange* | partial | dev/production-oriented* | partial | Consolidate with LAMICE |
| `LAMICE` | consolidating | orange* | beta/partial | dev/production-oriented* | partial | Creative Studio; share platform backend |
| `live-platform` | active | yellow* | partial | runtime-dependent | partial | Core Live Operations |
| `VBMF` | active | yellow* | implementation-in-progress* | specialized runtime | partial | Core Broadcast Fabric; preserve specialization |
| `video-shot-detection` | extract | yellow* | engine/prototype* | local/engine | partial | Standardize as Engine |
| `video-compression-system` | extract | yellow* | engine/prototype* | local/engine | partial | Standardize as Engine |
| `ai-spider-annotation` | consolidating | orange* | partial | dev | partial | Rebuild as Data Studio |
| `yimengjingshen` | active-lab | yellow* | research | lab | proven for research flows* | Keep as Research Lab |
| `xiao-opera-miniapp` | active | orange* | beta/mock portions* | miniapp | partial | Consumer Experience; replace mock AI |
| `media-platform` | frozen | red* | incomplete/legacy | legacy | documentary/partial | Migrate useful assets, do not extend |
| `YimengHeart` | legacy | red* | legacy | legacy | proven legacy behavior* | Compatibility then retire |

`*` = provisional assessment; must be replaced by repository-level evidence during the detailed audit.

## 3. Required evidence per repository

For each repository, the audit must capture:

1. default branch and latest verified commit;
2. package/runtime versions;
3. application entry points;
4. route inventory;
5. DB schema inventory;
6. queue/worker inventory;
7. storage providers and references;
8. auth and permission model;
9. real-vs-mock implementation map;
10. test inventory and actual passing evidence;
11. container/deployment path;
12. unresolved TODO/NotImplemented/fallback surfaces;
13. external dependency risks;
14. duplicate capabilities with other repositories;
15. reusable assets worth extracting;
16. explicit recommendation.

## 4. Completion score

Do not score completion by percentage of files or routes. Use end-to-end business slices.

For every important feature:

```text
Entry
→ API
→ State
→ Persistence
→ Worker/Runtime
→ Artifact/Result
→ Failure recovery
→ UI feedback
→ Test evidence
```

A slice is complete only when the chain is coherent.

## 5. Confidence labels

### Proven

Verified by code and execution/test evidence.

### Partially proven

Code exists and some validation exists, but important runtime or business-path evidence is missing.

### Documentary only

Claim appears in README/spec/roadmap but has not been verified in code/runtime.

### Contradicted

Documentation says feature exists, but source or runtime evidence shows it is missing, mocked, bypassed, or broken.

## 6. Audit update rule

Every new repository audit should append evidence, not overwrite history. When a provisional status changes, record:

```text
previous
new
reason
evidence
commit/ref
review date
```

This register is therefore an audit ledger, not a static scorecard.
