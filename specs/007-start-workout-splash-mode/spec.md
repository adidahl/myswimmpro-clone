# Feature Specification: Start Workout Menu and Splash Mode

**Feature Branch**: `007-start-workout-splash-mode`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 7 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Shared Workout Routes, Start Menu Pattern, Session Service.
- **Source screen clusters**: S008-S010, S014-S020, S061-S063, S097-S105, S194-S199.
- **Referenced screens**: S008, S009, S010, S061, S097, S098, S194, S195.
- **Explicitly out of scope**: Manual log save, watch sync implementation, PDF rendering, workout generation.

## User Scenarios & Testing

### User Story 1 - Open Start Menu (Priority: P1)

As a swimmer, I can open the Start Workout menu from any eligible workout detail and see consistent actions.

**Independent Test**: Open start menu from generated, custom, plan, and category workout contexts and compare available actions.

### User Story 2 - Start Splash Mode (Priority: P2)

As a swimmer, I can start a guided workout on the phone and see the active Splash Mode player.

**Independent Test**: Start Splash Mode from a fixture workout and return with back behavior matching source evidence.

### User Story 3 - Route Secondary Actions (Priority: P3)

As a swimmer, I can choose Manual Log, Send to Watch, or Open PDF from the start menu and reach the correct owning flow or placeholder.

**Independent Test**: Select each secondary action and verify ownership, safety, and return behavior.

## Requirements

- **FR-001**: Start Menu MUST show Start on this phone, Manual Log, Send To Watch, Open PDF, and Close where supported.
- **FR-002**: Splash Mode MUST render current set, up-next context, timer/progress, interval, effort, and controls placeholder.
- **FR-003**: Back from Splash Mode MUST return to the originating workout detail unless a later spec defines an exit confirmation.
- **FR-004**: Start Menu close MUST restore the underlying workout detail without mutation.
- **SR-001**: Workout unavailable, empty workout, orientation, pause/finish, and exit states MUST be defined.
- **SR-002**: Send To Watch and Open PDF MUST delegate to integration/export specs.

## Key Entities

- **StartMenuAction**: Available action and owning route.
- **WorkoutSessionState**: Active set, timer, progress, pause/finish state.
- **SplashModeViewState**: Player layout and control visibility.

## Success Criteria

- **SC-001**: Start Menu action contract is consistent across eligible workout contexts.
- **SC-002**: Splash Mode can start from a fixture workout and return safely.
- **SC-003**: Secondary actions route to owning placeholders without accidental final actions.

## Assumptions

- MVP player can use deterministic timer fixtures before full session persistence.
- Landscape layout behavior is part of planning and validation.
