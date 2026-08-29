# Platform Target State V1

## 1. Target ecosystem

```text
                       Media Digital Platform
                Experience / Identity / Workspace
                              |
             +----------------+----------------+
             |                                 |
      Business Control                 Intelligence Control
      news-media-system                Yimeng Intelligence
             |                                 |
       Content / Media                   AI / Knowledge
       Workflow / Publish                Evidence / Eval
             |                                 |
             +----------------+----------------+
                              |
                     Processing Plane
             Shot / Compress / ASR / OCR / QC
                              |
             +----------------+----------------+
             |                                 |
       Live Operations                   Broadcast Fabric
       live-platform                         VBMF
```

## 2. System of Record

- Business content truth: `news-media-system`.
- Canonical cross-system asset/artifact identity: shared contract and owning registry, with business ownership where appropriate.
- Runtime truth: each specialized runtime owns only its execution state.
- Knowledge truth: Yimeng Intelligence owns published knowledge artifacts and evidence indexes, while source content remains owned by its source system.
- Research truth: experiments and research datasets remain in the Research Lab until explicitly promoted.

## 3. Experience model

The user should perceive one product family:

```text
Content | Media | AI | Knowledge | Creative | Live | Broadcast | Data | Operations
```

The user should not need to understand repository boundaries.

## 4. Theme platform responsibilities

`media-digital-platform` SHOULD own:

- authentication/SSO integration
- workspace selection
- global navigation
- global search entry
- global notifications
- global task aggregation
- module/service registry
- deep-linking
- shared design system consumption

It MUST NOT own the internal business state of the domain systems.

## 5. Professional system responsibilities

### News Media

Own content, editorial workflow, publication, business users, sites and AI business governance.

### Yimeng Intelligence

Own model execution, knowledge ingestion, retrieval, evidence, evaluation and production AI artifacts.

### Creative Platform

Own creative project workflow, storyboard/timeline semantics, generation orchestration and media production.

### Live Platform

Own live-stream operational state and stream control abstractions.

### VBMF

Own broadcast-grade realtime media runtime and hardware/software fabric semantics.

### Processing Engines

Own specialist media transformations and derived artifacts.

## 6. Integration pattern

Preferred order:

1. synchronous versioned API for immediate business queries/commands;
2. asynchronous Job for long-running work;
3. Event for facts that downstream systems may react to;
4. direct database access only for controlled migration/forensics.

## 7. Migration posture

Old repositories should not be mounted as permanent dependencies merely to avoid rewriting them. Migration should extract domain assets and proven algorithms into the target owner.

## 8. Completion requirement

A target capability is considered production-ready only when:

```text
UX
→ API
→ state
→ runtime
→ result/artifact
→ recovery
→ tests
→ observability
→ security
→ real environment verification
```

are all demonstrated at the required evidence level.
