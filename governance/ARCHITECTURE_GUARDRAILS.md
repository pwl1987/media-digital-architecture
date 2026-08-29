# Architecture Guardrails V1

## Dependency direction

```text
Experience
   ↓
Business / Control
   ↓
Intelligence
   ↓
Processing
   ↓
Realtime Runtime
   ↓
Infrastructure
```

A lower layer MUST NOT depend on a higher business layer.

## Data ownership

- Business records are owned by the Business System of Record.
- AI systems may create derived artifacts but MUST NOT silently mutate business truth.
- Processing engines produce artifacts; they do not own user/project truth.
- Runtime systems own runtime state, not content metadata.

## Database rule

Cross-system access to another service's database is prohibited for production paths.
Use API or event contracts.

Read-only migration/forensics access is permitted during archaeology and migration.

## Canonical object rule

Every cross-system object MUST have one canonical owner and one stable identity namespace.

A local projection may exist, but it must carry provenance to the canonical identity.

## API rule

External business integrations use versioned contracts.
Model-native APIs such as OpenAI-compatible `/v1/*` are data-plane interfaces, not business contracts.

## Event rule

Events describe facts that already happened. Commands request work. Do not overload an event as a command.

Recommended naming:

```text
asset.created
asset.derived
job.queued
job.started
job.completed
job.failed
knowledge.published
model.released
generation.completed
```

## Job rule

`Task` is a business intent; `Job` is an execution instance. Retries create new Job attempts or explicit attempt records and must not mutate historical execution evidence.

## Artifact rule

Every generated file/result that may be referenced later should have an Artifact identity. URLs and storage paths are locators, not primary identities.

## AI result rule

Business-facing AI output should be represented as an `AIResult` containing result content plus model/provenance/evidence/usage/trace metadata as applicable.

## Frontend rule

Production apps may use different composition frameworks only by exception, but must consume the shared design language and interaction semantics.

Research UIs are not production design sources unless explicitly promoted.

## Exception rule

Any new deviation from these guardrails requires an ADR that states:

- problem
- alternatives
- decision
- scope
- trade-offs
- migration/rollback strategy
- owner
- review date
