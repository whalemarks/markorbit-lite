# Specification Alignment

This document explains how MarkOrbit Lite aligns with markorbit-core-specification at the module level.

## Alignment Rule

Each Lite module must map to a specification concept. If the specification defines a broader platform capability than Lite needs now, Lite implements only the application-scoped subset and reserves the rest.

## Mo Workspace

Specification  
↓  
Lite Implementation

Shared user, organization, membership, privacy, workspace context, persona, and knowledge concepts.  
↓  
Private agent workspace containing business profile, persona, knowledge, content preferences, price rules, materials, trademark assets, and lead context.

## Mo Content

Specification  
↓  
Lite Implementation

Content capability for planning, generation, reuse, and distribution support.  
↓  
Daily content topics, draft generation, template-assisted content, and publish-ready material preparation. Lite does not perform real external publishing automation.

## Mo Asset Hub

Specification  
↓  
Lite Implementation

Reusable media, templates, files, and content materials with ownership and usage metadata.  
↓  
Private and platform-provided assets used by content drafts, trademark listings, and recommendation material.

## Mo Assistant

Specification  
↓  
Lite Implementation

Action-oriented AI assistance over business context, capabilities, skills, and future workflows.  
↓  
Lite business-action assistant for content, trademark packaging, quotation, and lead follow-up. It uses local context and disabled Brain boundaries until Brain integration is authorized.

## Mo Marks

Specification  
↓  
Lite Implementation

Trademark asset, packaging, recommendation, inquiry, and transaction-support concepts.  
↓  
Agent-owned trademark assets, listing preparation, single-mark and multi-mark recommendation pages, and inquiry capture. Lite does not become a full marketplace.

## Mo Global

Specification  
↓  
Lite Implementation

Country service, pricing, quotation, and cross-border trademark service concepts.  
↓  
Quote plans and proposals built from available country services, country prices, and user price rules. Lite does not perform official filing or payment processing.

## Mo Leads

Specification  
↓  
Lite Implementation

Opportunity, customer communication, follow-up, campaign, and conversion concepts.  
↓  
Lead follow-up workspace with message drafts, communication logs, and actions that can progress opportunities toward quotes or orders.

## Brain Connector

Specification  
↓  
Lite Implementation

Brain-facing knowledge, rules, source, authorization, and connector contracts.  
↓  
Disabled connector strategy with metadata and authorization placeholders. No real Brain API, knowledge graph query, or private-data ingestion is implemented.

## Capability and Skill

Specification  
↓  
Lite Implementation

Capability definitions, skill implementations, and future registry/runtime semantics.  
↓  
Minimal Lite capability naming and application service mapping. No universal platform registry is required in Sprint 0.

## Workflow

Specification  
↓  
Lite Implementation

Workflow definitions, workflow runs, step runs, guide behavior, and flow execution.  
↓  
Reserved lightweight workflow concepts for content, recommendation, quotation, and lead follow-up. No full Workflow Runtime is implemented.
