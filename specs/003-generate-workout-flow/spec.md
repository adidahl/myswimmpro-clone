# Feature Specification: Generate Workout Flow

**Feature Branch**: `003-generate-workout-flow`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 3 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Workout Creation Routes, Generate Workout data flow, Workout Generator Service.
- **Source screen clusters**: S001-S035, especially S002-S007 and S011-S035.
- **Referenced screens**: S002, S003, S004, S005, S006, S007.
- **Explicitly out of scope**: Custom workout editor, saved library management, Splash Mode internals, real AI generation service tuning.

## User Scenarios & Testing

### User Story 1 - Complete Generation Wizard (Priority: P1)

As a swimmer, I can choose target distance and optional focus, strokes, equipment, and notes to request a generated workout.

**Independent Test**: Complete the five-step wizard with default and selected options and reach a generated workout detail placeholder.

### User Story 2 - Review Generated Result (Priority: P2)

As a swimmer, I can review the generated workout using the shared Workout Detail contract and decide whether to start, save, log, export, or chat.

**Independent Test**: Generate a result and confirm it routes into the shared detail surface with generated-unsaved context.

### User Story 3 - Swap Next Workout (Priority: P3)

As a swimmer with an active plan, I can enter the generator in replacement mode to swap the next workout without breaking plan context.

**Independent Test**: Open replacement mode from Home and confirm the result preserves the active-plan return route.

## Requirements

- **FR-001**: The system MUST provide wizard steps for distance, focus, strokes, equipment, and notes.
- **FR-002**: Optional steps MUST allow continuation without a selection when source evidence permits it.
- **FR-003**: Generate action MUST produce a normalized Workout result for shared Workout Detail.
- **FR-004**: Generated-unsaved workouts MUST expose Save to Library as an available action.
- **FR-005**: Replacement mode MUST record the active plan/workout context for return and swap handling.
- **SR-001**: Loading, generation failure, cancelled wizard, offline, and invalid input states MUST be defined.
- **SR-002**: Generation requests MUST not start a workout, save a workout, or replace a plan workout without explicit user action.

## Key Entities

- **WorkoutGenerationRequest**: Distance, focus, strokes, equipment, notes, and mode.
- **GeneratedWorkout**: Normalized Workout plus generated source metadata.
- **ReplacementContext**: Active plan and scheduled workout being swapped.

## Success Criteria

- **SC-001**: A reviewer can complete the generation wizard in under 90 seconds.
- **SC-002**: Generated result uses the shared Workout Detail contract with no duplicate detail implementation.
- **SC-003**: All optional wizard steps have documented skip/default behavior.

## Assumptions

- Early implementation may use deterministic fixtures before connecting a generator service.
- Notes remain optional and are not required for MVP generation.
