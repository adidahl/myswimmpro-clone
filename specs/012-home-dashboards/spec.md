# Feature Specification: Home Dashboards

**Feature Branch**: `012-home-dashboards`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 12 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Home Routes, Important Product States, MVP Sequencing.
- **Source screen clusters**: S001-S089, S142-S150, S222-S250.
- **Referenced screens**: S001, S143, S145, S147, S222, S223, S241, S245, S250.
- **Explicitly out of scope**: Generation internals, plan generation internals, completed detail internals, support content.

## User Scenarios & Testing

### User Story 1 - See Empty or Default Home (Priority: P1)

As a swimmer without an active plan or today's logged workout, I can see Home quick actions and support entry.

**Independent Test**: Open Home in default fixture state and verify create/generate/import/library/support links.

### User Story 2 - See Active Plan Home (Priority: P2)

As a swimmer with an active plan, I can see next workout, View, Swap, weekly streak, and training plan card.

**Independent Test**: Open Home in active-plan fixture state and route to next workout, swap, and plan detail placeholders.

### User Story 3 - See Post-Log Home (Priority: P3)

As a swimmer after logging a workout, I can see completion/streak confirmation, today's workout, updated next workout, and tab returns.

**Independent Test**: Open post-log fixture Home and verify today's workout and S247-S250 tab returns.

## Requirements

- **FR-001**: Home MUST support default, active-plan, and post-log dashboard states.
- **FR-002**: Default Home MUST link to Generate Workout, Custom Workout, Image Import, Saved Workout Library, Training Plan creation, tabs, and Support.
- **FR-003**: Active-plan Home MUST link View to next workout detail and Swap to generation replacement mode.
- **FR-004**: Post-log Home MUST link today's workout to Completed Workout Detail.
- **SR-001**: Loading, empty, partial data, offline, and stale post-log states MUST be defined.
- **SR-002**: Support close MUST return to Home.

## Key Entities

- **HomeDashboardState**: Default, active-plan, or post-log composition.
- **NextWorkoutCard**: Scheduled workout summary and action links.
- **TodayWorkoutCard**: Completed activity summary and detail target.
- **QuickAction**: Home creation or navigation shortcut.

## Success Criteria

- **SC-001**: All three Home states are independently demonstrable with fixtures.
- **SC-002**: Every Home action has an owning route or placeholder.
- **SC-003**: Post-log tab return behavior matches source evidence.

## Assumptions

- Home aggregation may read fixture state before backend services exist.
- Home owns composition, not feature-specific business logic.
