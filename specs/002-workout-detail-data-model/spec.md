# Feature Specification: Workout Data Model and Shared Detail

**Feature Branch**: `002-workout-detail-data-model`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 2 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Frontend Feature Modules, Shared Workout Routes, Core Domain Model, Backend Services, Workout Detail Action Pattern.
- **Source screen clusters**: S007-S035, S067-S074, S095-S112, S183-S201.
- **Referenced screens**: S007, S011, S068, S095, S193, S194.
- **Explicitly out of scope**: Workout generation, custom editing persistence, Splash Mode execution, manual logging, PDF rendering, real watch send.

## User Scenarios & Testing

### User Story 1 - View Any Workout Detail (Priority: P1)

As a swimmer, I can open a workout from generated, saved, WOD, category, or plan context and see a consistent detail surface with title, stats, pool length, sections, sets, and primary actions.

**Independent Test**: Open representative placeholder workouts from at least two source contexts and confirm the same detail contract appears with source-specific back behavior.

### User Story 2 - Use Shared Workout Actions (Priority: P2)

As a swimmer, I can access the same action contract on supported workout details: start menu, overflow actions, Coach Chat, section expand/collapse, and pool length controls.

**Independent Test**: Open a workout detail and verify each visible action either routes to the owning placeholder or is safely blocked if the owning package is not implemented.

### User Story 3 - Preserve Editable Context Boundaries (Priority: P3)

As a swimmer editing or viewing workouts, I can distinguish read-only detail actions from editable custom workout controls.

**Independent Test**: Compare generated/saved detail placeholders with custom workout detail placeholders and confirm editable section overflow is only available where allowed.

## Requirements

- **FR-001**: The system MUST define a canonical Workout entity with sections, set groups, sets, source, stats, pool length, category, strokes, equipment, and ownership context.
- **FR-002**: The shared Workout Detail surface MUST render generated, saved, WOD, category, plan, and completed-workout source variants without duplicating the core contract.
- **FR-003**: The detail surface MUST expose Start Workout, More, Coach Chat, navigate-up, pool-length controls, and section controls where supported by source evidence.
- **FR-004**: Overflow menus MUST list only actions supported by the current workout context and safety rules.
- **FR-005**: Editable section actions MUST be isolated to custom/editable contexts.
- **SR-001**: Loading, empty workout, missing workout, unsupported source, and back-return states MUST be defined.
- **SR-002**: Reset/delete/log/share/send actions MUST be represented as risky or owned by later specs.

## Key Entities

- **Workout**: Shared workout definition and metadata.
- **WorkoutSection**: Named section such as Warm Up, Drill Set, Main Set, Cool Down.
- **SetGroup**: Repeat/group settings and ordered sets.
- **WorkoutSet**: Distance, repetition, stroke, interval, effort, notes, and equipment.
- **WorkoutDetailContext**: Source context, editability, available actions, and return route.

## Success Criteria

- **SC-001**: One shared detail contract supports at least five source contexts without changing primary action semantics.
- **SC-002**: 100% of risky actions are mapped to confirmation-gated or placeholder destinations.
- **SC-003**: Back behavior is documented for each source context used by this spec.

## Assumptions

- The workout model can be implemented with local fixtures before API services exist.
- Business logic for generating, saving, logging, and exporting is delegated to owning specs.
