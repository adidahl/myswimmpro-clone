# Feature Specification: Library Browsing and Catalogs

**Feature Branch**: `010-library-browse-catalogs`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 10 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Library Routes, Workout Library module, Training Plans module.
- **Source screen clusters**: S151-S175, S182-S193, plus S115.
- **Referenced screens**: S115, S151, S154, S158, S162, S165, S168, S183, S189, S193.
- **Explicitly out of scope**: Saved library management, plan generation internals, workout detail internals beyond shared route links.

## User Scenarios & Testing

### User Story 1 - Browse Library Home (Priority: P1)

As a swimmer, I can open the Library tab and see saved workout preview, create actions, WOD preview/history, training plan entry, and workout categories.

**Independent Test**: Open Library and verify every major section links to the correct route placeholder.

### User Story 2 - Browse Workout Lists and Filters (Priority: P2)

As a swimmer, I can open WOD history and category lists and apply filter sheets.

**Independent Test**: Open Freestyle and Distance categories, filter sheets, and return paths.

### User Story 3 - Browse Plan Catalog Entry Points (Priority: P3)

As a swimmer, I can reach training plan catalog and template detail placeholders from Library.

**Independent Test**: Open plan catalog and template detail, then return to Library.

## Requirements

- **FR-001**: Library tab MUST provide sections for saved workouts, create actions, WOD, training plans, and workout categories.
- **FR-002**: WOD history and category lists MUST link to shared Workout Detail.
- **FR-003**: Category filter sheet MUST expose distance, duration, skill level, and workout type controls.
- **FR-004**: Plan catalog links MUST delegate to the Training Plans spec.
- **SR-001**: Empty lists, loading, filter no-results, offline, and return states MUST be defined.
- **SR-002**: Support entry from Library MUST return to Library on close.

## Key Entities

- **LibrarySection**: Saved preview, create cards, WOD, plans, categories.
- **WorkoutListQuery**: Category and filter state.
- **WorkoutOfDayEntry**: WOD list item and detail target.
- **PlanCatalogPreview**: Library plan entry and template link.

## Success Criteria

- **SC-001**: All Library sections have route targets or explicit placeholders.
- **SC-002**: Category filter state is inspectable and resettable.
- **SC-003**: WOD/category detail links reuse shared Workout Detail.

## Assumptions

- Catalog lists may use fixtures before API/BFF integration.
- Support article exploration remains low priority.
