# Feature Specification: Custom Workout Editor

**Feature Branch**: `004-custom-workout-editor`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 4 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Workout Creation Routes, Workout Builder Service, Shared Interaction Patterns.
- **Source screen clusters**: S036-S066.
- **Referenced screens**: S036, S037, S052, S053, S056, S059, S061.
- **Explicitly out of scope**: Generated workouts, image import OCR, final save persistence beyond save-to-library contract, full Splash Mode internals.

## User Scenarios & Testing

### User Story 1 - Start a Custom Workout Draft (Priority: P1)

As a swimmer, I can open a blank custom workout editor with editable sections and shared workout actions.

**Independent Test**: Open the editor from Home/Library and confirm the draft shell, section menu, and action hosts are present.

### User Story 2 - Edit Sections, Groups, and Sets (Priority: P2)

As a swimmer, I can add sets, add set groups, edit group settings, and cancel edits without accidental draft mutation.

**Independent Test**: Open each editor dialog, cancel it, and confirm the draft returns unchanged.

### User Story 3 - Use Custom Workout Actions (Priority: P3)

As a swimmer, I can start, log, export, save, or chat from a custom workout only when the draft state supports that action.

**Independent Test**: Verify unsupported actions on empty drafts are blocked or no-op exactly as specified.

## Requirements

- **FR-001**: The system MUST represent a custom workout draft with sections, set groups, sets, pool length, title, and editability state.
- **FR-002**: Section overflow MUST support Add Set, Add Set Group, Group Settings, and Delete Set Group where allowed.
- **FR-003**: Add/edit dialogs MUST support cancel without mutation.
- **FR-004**: Draft validation MUST prevent invalid empty or malformed workout persistence.
- **FR-005**: Shared Workout Detail actions MUST be available through the same contract as other workout contexts.
- **SR-001**: Delete Set Group and final save actions MUST be confirmation-gated or safely blocked.
- **SR-002**: Empty draft, invalid set, invalid interval, cancelled edit, and back-return states MUST be defined.

## Key Entities

- **WorkoutDraft**: Editable workout-in-progress.
- **DraftSection**: Editable section container.
- **DraftSetGroup**: Editable set group and repeat metadata.
- **DraftSet**: Editable set details and validation state.
- **DraftMutation**: Add, edit, delete, save, or cancel operation.

## Success Criteria

- **SC-001**: A reviewer can open and cancel every editor dialog without changing the draft.
- **SC-002**: Invalid draft states are blocked before persistence.
- **SC-003**: Custom workout actions reuse shared workout route hosts.

## Assumptions

- MVP can use local draft state before server persistence exists.
- Deleting draft content is treated as risky even if the draft has not been saved.
