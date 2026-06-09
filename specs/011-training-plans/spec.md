# Feature Specification: Training Plans

**Feature Branch**: `011-training-plans`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 11 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Training Plan Routes, Training Plan Generation data flow, Training Plan Service.
- **Source screen clusters**: S081-S114, S158-S161, S188-S190.
- **Referenced screens**: S081, S084, S086, S090, S091, S094, S097, S159, S189.
- **Explicitly out of scope**: Workout Detail internals, Splash Mode internals, completed activity logging internals.

## User Scenarios & Testing

### User Story 1 - Generate a Personalized Plan (Priority: P1)

As a swimmer, I can choose goals, plan length, swim days, yardage/notes, and generate a plan candidate.

**Independent Test**: Complete plan generation wizard with valid choices and reach plan detail.

### User Story 2 - View and Start a Plan (Priority: P2)

As a swimmer, I can view plan overview, weekly volume, week workouts, and start a plan.

**Independent Test**: Open generated and template plan details and confirm start behavior is explicit.

### User Story 3 - Use Active Plan Workouts (Priority: P3)

As a swimmer, I can open a plan workout through shared Workout Detail and return to plan context.

**Independent Test**: Open a plan workout, use shared actions, and return to plan detail.

## Requirements

- **FR-001**: Plan wizard MUST capture goal, plan length/pool context, swim days, weekly volume or notes, and generate action.
- **FR-002**: Plan Detail MUST show overview, weekly volume, week list, and workout entries.
- **FR-003**: Template and generated plans MUST share the plan detail contract where applicable.
- **FR-004**: Starting, replacing, creating new, or cancelling active plans MUST be confirmation-gated when it changes active plan state.
- **FR-005**: Plan workout links MUST reuse shared Workout Detail with plan context.
- **SR-001**: No swim days, generation failure, existing active plan, cancel plan, offline, and return states MUST be defined.

## Key Entities

- **TrainingPlan**: Template or generated plan.
- **TrainingPlanEnrollment**: Active plan state and progress.
- **PlanWeek**: Week grouping and volume.
- **ScheduledWorkout**: Plan assignment and linked Workout.
- **PlanGenerationRequest**: Wizard inputs and constraints.

## Success Criteria

- **SC-001**: A fixture plan can be generated or opened and inspected end to end.
- **SC-002**: Active-plan mutation actions are confirmation-gated.
- **SC-003**: Plan workouts retain plan return context.

## Assumptions

- Early plan generation may use deterministic fixtures.
- One active plan at a time is the default unless clarified later.
