# Feature Specification: Cross-App QA Matrix

**Feature Branch**: `018-qa-matrix`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 18 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md PRD Checklist, Risky / Final Actions, Important Product States, Source Screen Clusters.
- **Source screen clusters**: All clusters listed in APP_ARCHITECTURE.md Source Screen Clusters.
- **Referenced screens**: S001-S250 through manual-navigation-map/NAVIGATION.md, screenshots, and states.
- **Explicitly out of scope**: Implementing feature behavior; this spec defines validation coverage and acceptance gates.

## User Scenarios & Testing

### User Story 1 - Validate Risky Actions (Priority: P1)

As a reviewer, I can audit every destructive, account-changing, transmitting, or external action and confirm it is blocked, confirmation-gated, or safely represented.

**Independent Test**: Run the risky-action matrix against all specs and verify no final action is unowned.

### User Story 2 - Validate Navigation Returns (Priority: P2)

As a reviewer, I can validate every mapped branch returns to the expected source screen or tab.

**Independent Test**: Compare route return behavior against source screen pairs in NAVIGATION.md.

### User Story 3 - Validate Shared Flow Duplicates (Priority: P3)

As a reviewer, I can detect duplicate implementations of shared surfaces and confirm one shared contract owns each.

**Independent Test**: Audit Workout Detail, Start Menu, Splash Mode, Manual Log, PDF, Coach Chat, Support, and native leaves across all feature plans.

## Requirements

- **FR-001**: QA matrix MUST enumerate risky/final actions and owning specs.
- **FR-002**: QA matrix MUST enumerate empty, active, post-log, loading, error, offline, permission denied, and return states where applicable.
- **FR-003**: QA matrix MUST map shared surfaces to owning feature specs and consumer specs.
- **FR-004**: QA matrix MUST include navigation evidence references for source screen IDs.
- **FR-005**: QA matrix MUST define pass/fail criteria before implementation completion.
- **SR-001**: Any unmapped risky action or unowned shared surface is a blocking issue before implementation.

## Key Entities

- **QACheck**: Validation item, scope, evidence, owner, and status.
- **RiskyActionInventory**: Destructive/final actions and gating requirements.
- **NavigationReturnPair**: Source route, target route, action, and expected return.
- **SharedSurfaceInventory**: Shared component/flow owner and consumers.

## Success Criteria

- **SC-001**: 100% of work package specs map to at least one QA matrix section.
- **SC-002**: 100% of risky/final action categories from APP_ARCHITECTURE.md have QA checks.
- **SC-003**: Shared surfaces have one owner and documented consumers.

## Assumptions

- QA matrix is maintained as a living artifact while plans and tasks evolve.
- Detailed automated test implementation belongs to each owning feature plan.
