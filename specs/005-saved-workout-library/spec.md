# Feature Specification: Saved Workout Library

**Feature Branch**: `005-saved-workout-library`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 5 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Library Routes, Workout Catalog Service, SavedWorkout entity.
- **Source screen clusters**: S067-S074, S152-S153, and save dialogs S012-S013, S041-S042.
- **Referenced screens**: S012, S013, S067, S068, S072, S152.
- **Explicitly out of scope**: Full workout browsing categories, WOD history, plan catalog, generation internals.

## User Scenarios & Testing

### User Story 1 - View Saved Workouts (Priority: P1)

As a swimmer, I can open My Workout Library and see saved workouts with summary information.

**Independent Test**: Open saved workouts from Home and Library entry points and confirm list and item navigation.

### User Story 2 - Save a Workout to Library (Priority: P2)

As a swimmer, I can save an eligible generated or custom workout to my library with a title.

**Independent Test**: Open Add to Library dialog, cancel and confirm no save, then save with a valid title in a controlled fixture.

### User Story 3 - Delete a Saved Workout Safely (Priority: P3)

As a swimmer, I can access delete for saved workouts only through a confirmation-gated flow.

**Independent Test**: Open item overflow and confirm Delete is represented as risky and cannot execute without confirmation.

## Requirements

- **FR-001**: The system MUST list saved workouts with title, distance, duration, level/category, and overflow.
- **FR-002**: Saved workout item selection MUST open shared Workout Detail with saved context.
- **FR-003**: Eligible workout details MUST expose Add to Library dialog with title input.
- **FR-004**: Save cancellation MUST leave the library unchanged.
- **FR-005**: Duplicate save behavior MUST be defined before implementation.
- **SR-001**: Delete saved workout MUST be confirmation-gated.
- **SR-002**: Empty library, loading, save failure, duplicate title, offline, and return states MUST be defined.

## Key Entities

- **SavedWorkout**: User-owned reference or copy of a Workout.
- **SaveToLibraryRequest**: Source workout and chosen title.
- **SavedWorkoutListState**: List, empty, loading, error, and filter context.

## Success Criteria

- **SC-001**: A saved workout can be reached from list to detail and back with correct context.
- **SC-002**: Delete cannot execute without explicit confirmation.
- **SC-003**: Add-to-library cancel and save paths have separate acceptance criteria.

## Assumptions

- Initial data may include seeded saved workouts from the navigation evidence.
- Server persistence can be added after list/detail contracts are stable.
