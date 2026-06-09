# Feature Specification: Profile, Achievements, and History

**Feature Branch**: `014-profile-achievements-history`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 14 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Profile Routes, Profile module, Achievement Service, Activity Log Service.
- **Source screen clusters**: S117-S141, S180, S249, plus completed-history links S222-S240.
- **Referenced screens**: S117, S133, S134, S136, S137, S140, S180, S249.
- **Explicitly out of scope**: Settings account details, completed workout edit/share internals, support article content.

## User Scenarios & Testing

### User Story 1 - Navigate Profile Tabs (Priority: P1)

As a swimmer, I can switch between History, Performance, and Swim Profile tabs.

**Independent Test**: Open Profile and visit each tab with fixture data.

### User Story 2 - View History and Achievements (Priority: P2)

As a swimmer, I can see lifetime counters, completed workouts, achievements preview, achievement grid, and achievement detail.

**Independent Test**: Open achievements grid/detail and return to Profile.

### User Story 3 - Review Swim Profile Preferences (Priority: P3)

As a swimmer, I can view editable swim preferences and seed times without accidental save.

**Independent Test**: Open Swim Profile tab and confirm save/edit actions are gated by a later settings/profile-edit contract.

## Requirements

- **FR-001**: Profile MUST provide History, Performance, and Swim Profile tabs.
- **FR-002**: History MUST show lifetime counters, completed workouts, and achievements preview.
- **FR-003**: Performance MUST show seed-time cards by stroke/distance.
- **FR-004**: Swim Profile MUST show seed times, swim days, and preferred workout length.
- **FR-005**: Achievements grid and detail MUST support return to Profile.
- **SR-001**: Profile edit/save actions MUST be treated as final account changes.
- **SR-002**: Empty history, no achievements, loading, offline, and support return states MUST be defined.

## Key Entities

- **SwimProfile**: Seed times, preferences, swim days, privacy flags.
- **Achievement**: Badge metadata and unlock criteria.
- **AchievementEarned**: User-earned badge state.
- **ProfileMetricSummary**: Lifetime and performance counters.

## Success Criteria

- **SC-001**: All Profile tabs are independently reachable.
- **SC-002**: Achievement grid/detail return behavior is documented.
- **SC-003**: Profile edit/save is not executed accidentally from view-only surfaces.

## Assumptions

- Profile data can be fixture-backed before account service implementation.
- Detailed preference editing may be split into a later profile-edit plan if needed.
