# Implementation Foundation

## Clean Start Principles

- Treat Lite as a new implementation.
- Do not copy V1 code or product structure.
- Use Mo Architecture and Lite planning documents as the foundation.
- Keep Sprint 0 limited to governance documents.

## Selective Reuse Principles

- Reuse proven business ideas only when they support Lite positioning.
- Revalidate each reused concept against workspace-first execution.
- Prefer concept reuse over implementation reuse.
- Do not inherit legacy constraints without an explicit decision.

## Repository Conventions

- Keep architecture, alignment, charter, implementation, and review documents under `docs/`.
- Record major architectural decisions under `docs/adr/`.
- Keep planning governance under `docs/planning/`.
- Keep sprint reports under `docs/review/`.
- Do not create application code, schemas, migrations, APIs, or UI during foundation-only tasks.

## Layer Responsibilities

- Application layer: Lite user experience and business actions.
- Domain layer: Lite business concepts and invariants.
- Integration layer: external service and future Mo connector boundaries.
- Data layer: persistence only after schema tasks are explicitly approved.
- Governance layer: documents, ADRs, alignment, and release constraints.

## Workspace-First Strategy

The workspace is the default context for content, assets, trademarks, quotes, leads, persona, knowledge, and preferences. User and organization data remain private unless future authorization explicitly allows sharing.

## Brain Disabled Strategy

Brain is reserved but disabled. Lite may define disabled connectors, source metadata, and authorization placeholders. Lite must not call real Brain services or ingest private workspace data into Brain during foundation work.

## Workflow Reserved Strategy

Workflow concepts are reserved for future orchestration. Lite may name flows and steps, but it must not implement a general Workflow Runtime until that work is explicitly planned.

## Future Runtime Compatibility

Lite services should remain replaceable by future Runtime execution. Avoid embedding hidden registries, platform runtimes, or irreversible coupling inside application code.
