# MarkOrbit Lite Architecture

## Lite Positioning

MarkOrbit Lite is the first usable application layer for Mo capabilities. It is a clean-start product for trademark agents, focused on daily business execution: content, assets, trademark recommendation, quotation, lead follow-up, and order conversion.

Lite is not the full Mo platform. It is a bounded application that makes selected Mo concepts usable before the full Mo Data, Brain, Workflow Runtime, and Runtime layers exist.

## Relationship with Mo Architecture

Lite follows the Mo Architecture chain:

```text
Data → Brain → Intelligence → Capability → Skill → Workflow → Guide → Flow → Applications
```

Lite lives in the Applications layer. It exposes agent-facing workflows and prepares integration points for upstream Mo capabilities without implementing the full architecture internally.

## Relationship with markorbit-core-specification

The markorbit-core-specification is the governance source for shared MarkOrbit concepts, names, module boundaries, capability semantics, and future compatibility expectations.

Lite implements only the parts needed by the Lite application boundary and maps each major module back to the specification. Where the specification describes future platform behavior, Lite reserves interfaces rather than building premature infrastructure.

## Relationship with Future Runtime

Lite must remain compatible with a future Runtime that can execute capabilities, skills, workflows, policy checks, and cross-application actions.

Until that Runtime exists, Lite may use explicit application services and lightweight orchestration, but these must not become hidden platform runtimes.

## Relationship with Brain

Mo Brain is disabled for Lite foundation work. Lite may define Brain-facing boundaries such as connector contracts, authorization intent, source metadata, and disabled connector behavior.

Lite must not automatically upload private user workspace data to Brain. User data remains private unless an explicit future authorization model allows sharing.

## Relationship with Workflow Runtime

Lite may model business actions with workflow-like terminology, but it does not implement a full Workflow Runtime in Sprint 0.

Workflow concepts are reserved for future content, recommendation, quotation, and lead follow-up flows. Early Lite implementation should stay simple and replaceable.

## Application Boundaries

Lite owns:

- user and organization workspace experience;
- private business profile, persona, knowledge, preferences, and materials;
- content planning and drafting experience;
- media and template asset usage within Lite;
- trademark packaging and recommendation pages;
- quotation plan preparation using available country service and price data;
- opportunity follow-up drafts and conversion actions;
- application-level auditability and privacy boundaries.

Lite does not own:

- global trademark data infrastructure;
- full Mo Brain knowledge graph;
- platform-wide intelligence engine;
- universal capability registry;
- general-purpose Workflow Runtime;
- official filing, payment, escrow, or service-provider marketplace infrastructure;
- MarkOrbit V1 legacy implementation structure.
