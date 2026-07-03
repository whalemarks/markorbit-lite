# ADR-001: Clean Start + Selective Reuse

Status: Accepted  
Date: 2026-07-03

## Context

MarkOrbit Lite is the first usable application layer for Mo capabilities. It must serve trademark agents with a workspace-first product experience while preserving compatibility with the long-term Mo Architecture.

MarkOrbit V1 proved important business ideas, but it also accumulated product and implementation constraints that do not match Lite's new role as a clean Mo application layer.

## Decision

Lite will be rebuilt as a clean-start implementation.

Lite may selectively reuse proven business ideas from V1, including user workspace concepts, trademark asset operations, opportunity follow-up, global quotation, AI-assisted actions, and order conversion patterns.

Lite must not inherit V1 code, database assumptions, navigation structure, or implementation shortcuts by default.

## Rationale

A clean start allows Lite to:

- align directly with Mo Architecture instead of retrofitting legacy structure;
- keep the first release focused on the agent workspace and daily business actions;
- avoid carrying V1's menu-driven product shape into Lite;
- preserve clear boundaries between application, Brain, Workflow Runtime, and future Runtime;
- establish implementation governance before application code begins.

Selective reuse keeps Lite practical by retaining validated business learning without copying legacy implementation.

## Consequences

- Planning knowledge may inform Lite, but V1 is not the source of architectural truth.
- New implementation must justify each reused idea against Lite positioning and Mo alignment.
- Lite Sprint 0 foundation work produces governance documents only.
- Application code, schema, migrations, APIs, and UI are intentionally out of scope for this decision.
