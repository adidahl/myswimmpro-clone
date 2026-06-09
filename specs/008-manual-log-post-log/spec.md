# Feature Specification: Manual Log and Post-Log Updates

**Feature Branch**: `008-manual-log-post-log`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 8 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Manual Log data flow, Activity Log Service, Important Product States.
- **Source screen clusters**: S015-S016, S029-S030, S100-S102, S200-S201, S222-S250.
- **Referenced screens**: S015, S101, S200, S201, S222, S247-S250.
- **Explicitly out of scope**: Completed workout share/edit/PDF details, trends metric algorithms beyond post-log refresh hooks.

## User Scenarios & Testing

### User Story 1 - Open Manual Log (Priority: P1)

As a swimmer, I can open Manual Log from a workout and see prefilled workout details.

**Independent Test**: Open Manual Log from generated, plan, and category contexts and confirm prefilled fields.

### User Story 2 - Save a Completed Activity (Priority: P2)

As a swimmer, I can save a manual log and see the app move into a post-log state.

**Independent Test**: Save a fixture log and confirm Home, Profile, Trends, and Library tab returns reflect post-log state.

### User Story 3 - Cancel or Back Out Safely (Priority: P3)

As a swimmer, I can back out of Manual Log without creating an activity.

**Independent Test**: Open Manual Log, back out, and verify no completed workout appears.

## Requirements

- **FR-001**: Manual Log MUST prefill title, distance, duration, date, notes, and image/set controls where available.
- **FR-002**: Save MUST create an ActivityLog only after explicit user action.
- **FR-003**: Post-log state MUST update Home, Profile History, Trends, achievements, and streak surfaces through documented refresh hooks.
- **FR-004**: Back/cancel MUST not create or modify an activity.
- **SR-001**: Invalid distance/duration/date, save failure, offline, duplicate save, and unsaved changes states MUST be defined.
- **SR-002**: Save is a final account-changing action and MUST have clear confirmation or completion feedback.

## Key Entities

- **ManualLogDraft**: Prefilled and editable log form state.
- **ActivityLog**: Completed swim activity.
- **PostLogRefresh**: Home/Profile/Trends/Achievement recalculation trigger.

## Success Criteria

- **SC-001**: A fixture log can be saved and discovered from post-log Home/Profile paths.
- **SC-002**: Cancel/back paths produce no ActivityLog.
- **SC-003**: Post-log tab returns match S247-S250 behavior.

## Assumptions

- Metric recalculation may be fixture-backed before analytics services exist.
- Manual Log owns creating activities; workout detail only links into it.
