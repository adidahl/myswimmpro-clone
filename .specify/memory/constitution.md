<!--
Sync Impact Report
Version change: template -> 1.0.0
Modified principles:
- PRINCIPLE_1_NAME -> I. Evidence-Backed Product Scope
- PRINCIPLE_2_NAME -> II. Shared Flow and Domain Reuse
- PRINCIPLE_3_NAME -> III. Pre-Implementation Analysis Gates
- PRINCIPLE_4_NAME -> IV. Traceable Validation
- PRINCIPLE_5_NAME -> V. Risky Action and Privacy Safety
Added sections:
- Product Planning Sources
- Development Workflow
Removed sections:
- None
Templates requiring updates:
- updated: .specify/templates/spec-template.md
- updated: .specify/templates/plan-template.md
- updated: .specify/templates/tasks-template.md
- updated: AGENTS.md
Follow-up TODOs:
- None
-->

# MySwimPro Clone Constitution

## Core Principles

### I. Evidence-Backed Product Scope

Every feature specification MUST cite the relevant source evidence from
APP_ARCHITECTURE.md and manual-navigation-map/NAVIGATION.md before planning.
Specs MUST list the source screen clusters, important screen IDs, and explicit
out-of-scope flows. Agent-created behavior that is not grounded in these
sources is not acceptable unless the spec records it as a deliberate product
decision.

Rationale: this project is reconstructing a mapped product surface. The
navigation map, state dumps, and screenshots are the evidence that keeps agent
work aligned with the observed app instead of invented behavior.

### II. Shared Flow and Domain Reuse

Shared surfaces MUST be specified and implemented once, then reused through
feature boundaries. Workout Detail, Start Menu, Splash Mode, Manual Log, PDF
export, Coach Chat, Training Plan Detail, support leaves, and native share/photo
leaves MUST keep consistent action contracts wherever they appear.

Rationale: APP_ARCHITECTURE.md identifies these as shared feature surfaces.
Duplicating them across packages would create navigation drift, inconsistent
state handling, and avoidable rework.

### III. Pre-Implementation Analysis Gates

Implementation MUST NOT begin until the active feature has a completed spec,
requirements quality checklist, implementation plan, generated task list, and
cross-artifact analysis report. Clarification MUST run before planning whenever
the spec contains ambiguous scope, state, safety, privacy, or navigation
decisions. Plans and tasks MUST resolve all NEEDS CLARIFICATION markers before
implementation.

Rationale: the project goal is to decompose work to the smallest useful detail
before agents write code. The gates make that discipline explicit and repeatable.

### IV. Traceable Validation

Every user story MUST be independently testable and traceable from user goal to
requirements, source screens, plan artifacts, tasks, and validation steps.
Feature plans MUST define state coverage for loading, empty, success, error,
permission denied, offline, and navigation return behavior when applicable.
Tasks MUST include exact file paths and validation commands or manual checks.

Rationale: traceability lets multiple agents work safely in parallel and makes
it possible to audit whether implementation still matches the mapped product.

### V. Risky Action and Privacy Safety

Risky or final actions MUST be confirmation-gated or modeled as leaf actions in
specs and tasks. This includes delete, logout, cancel plan/subscription, account
data export/deletion, profile/settings save, completed-workout save/edit, app
review submission, support/coach message send, native share target selection,
diagnostic log send, integration toggles, and any action that transmits content
outside the app.

Rationale: the source mapping intentionally avoided destructive and transmitting
actions. Implementation agents must preserve that safety posture unless a spec
explicitly defines the confirmation and recovery behavior.

## Product Planning Sources

APP_ARCHITECTURE.md is the architecture backbone for product modules, routes,
domain entities, service boundaries, suggested agent work packages, MVP
sequencing, and PRD checklist expectations. manual-navigation-map/NAVIGATION.md
is the navigation evidence ledger and MUST be consulted for source screen IDs,
branch status, safe/risky action notes, and screenshot/state references.

Feature specs SHOULD cite local screenshots or state dumps when the UI contract
depends on observed layout, visible copy, menu contents, or native leaf behavior.
Support article content is low priority unless explicitly requested.

## Development Workflow

Work SHOULD be split according to the Suggested Agent Work Packages in
APP_ARCHITECTURE.md unless a feature spec records a smaller, independently
testable boundary. Each Spec Kit feature directory MUST remain reviewable as an
artifact package: spec.md, checklists, plan.md, research.md, data-model.md,
contracts, quickstart.md, tasks.md, and analyze output when produced.

Agents MUST prefer MVP-first sequencing. User Story 1 should be independently
demonstrable before later stories are implemented. Shared foundations may be
created in Phase 1 or Phase 2 only when they are required by multiple stories
and are justified in the plan.

## Governance

This constitution supersedes ad hoc prompting, generated plans, and task lists.
If a spec, plan, or task conflicts with a MUST principle, the artifact must be
updated before implementation proceeds. Constitution changes require an explicit
version bump, a Sync Impact Report, and review of dependent templates.

Versioning follows semantic versioning:
- MAJOR for removing or redefining principles in a backward-incompatible way.
- MINOR for adding principles, gates, or materially broader governance.
- PATCH for clarifications that do not change compliance expectations.

Compliance review is required at each Spec Kit gate: constitution, specify,
clarify when needed, checklist, plan, tasks, analyze, and implementation.

**Version**: 1.0.0 | **Ratified**: 2026-06-09 | **Last Amended**: 2026-06-09
