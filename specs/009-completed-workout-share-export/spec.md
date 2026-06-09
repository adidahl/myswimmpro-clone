# Feature Specification: Completed Workout Detail, Share, Edit, and Export

**Feature Branch**: `009-completed-workout-share-export`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 9 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Completed Workout Routes, Completed Workout Sharing data flow, Export/Share module.
- **Source screen clusters**: S222-S246.
- **Referenced screens**: S222, S225, S226, S227, S231, S235, S238.
- **Explicitly out of scope**: Manual log creation, external share target transmission, low-level PDF renderer internals.

## User Scenarios & Testing

### User Story 1 - View Completed Workout (Priority: P1)

As a swimmer, I can open today's or historical completed workout detail and see activity stats and actions.

**Independent Test**: Open completed workout detail from Home and return safely.

### User Story 2 - Edit Completed Workout (Priority: P2)

As a swimmer, I can open an edit form and save or cancel changes safely.

**Independent Test**: Open edit, cancel without mutation, then save fixture edits with validation.

### User Story 3 - Share or Export Completed Workout (Priority: P3)

As a swimmer, I can preview social share visuals and PDF export before selecting native share targets.

**Independent Test**: Open share preview and PDF preview; back out from native share sheets without transmission.

## Requirements

- **FR-001**: Completed Workout Detail MUST show activity summary, source workout details, and More actions.
- **FR-002**: Edit form MUST validate mutable activity fields before saving.
- **FR-003**: Social share preview MUST support visual customization before native share handoff.
- **FR-004**: Completed-workout PDF preview MUST open before native share handoff.
- **SR-001**: Delete, edit save, native share target, and PDF share are risky/final actions and MUST be gated.
- **SR-002**: Missing activity, edit conflict, export failure, share cancel, and back-return states MUST be defined.

## Key Entities

- **CompletedWorkoutDetail**: ActivityLog plus display stats and actions.
- **CompletedWorkoutEditDraft**: Editable activity fields and validation state.
- **ShareArtifact**: Social image or PDF metadata and preview state.

## Success Criteria

- **SC-001**: Completed detail can be opened from Home and returned from without losing context.
- **SC-002**: Native share sheets can be opened and dismissed without transmission.
- **SC-003**: Edit cancel and edit save have separate documented outcomes.

## Assumptions

- Export output can be fixture-backed until renderer quality is addressed.
- Native share target selection remains outside this feature's automated tests.
