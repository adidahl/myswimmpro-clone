# Feature Specification: External Integrations and Export Boundaries

**Feature Branch**: `017-external-integrations-export`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 17 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Export/Share module, External Integrations, Share Service, Device Integration Service, Legal/Compliance Service.
- **Source screen clusters**: S019, S021-S023, S032, S045-S046, S051, S103-S109, S121-S124, S129-S131, S227-S233.
- **Referenced screens**: S019, S022, S045, S051, S107, S121, S123, S129, S227, S232.
- **Explicitly out of scope**: Selecting native share targets, real watch transfer, real app review submission, billing provider execution.

## User Scenarios & Testing

### User Story 1 - Preview Exports Before Sharing (Priority: P1)

As a swimmer, I can open workout or completed-workout PDF/social previews before choosing any native share target.

**Independent Test**: Open PDF and social preview placeholders and back out.

### User Story 2 - Trigger External Boundaries Safely (Priority: P2)

As a swimmer, I can reach watch send, native share, review, and legal boundaries without accidental transmission or mutation.

**Independent Test**: Open each boundary and confirm no final external action happens without explicit selection.

### User Story 3 - Manage Integration Connection Boundaries (Priority: P3)

As a swimmer, I can view external integration connection points for watch, Strava, Garmin, Health Connect, and TrainingPeaks.

**Independent Test**: Open each provider placeholder and return safely.

## Requirements

- **FR-001**: Export previews MUST appear before native share target selection.
- **FR-002**: Send To Watch MUST report or route to integration state without assuming a connected device.
- **FR-003**: Native share, app review, legal WebView, subscription, and provider auth boundaries MUST be modeled as explicit leaves.
- **FR-004**: Share metadata MUST distinguish preview state from transmitted state.
- **SR-001**: Native target selection, provider authorization, review submission, and subscription management are final/external actions and MUST be gated.
- **SR-002**: Provider unavailable, permission denied, cancelled external flow, export failure, and offline states MUST be defined.

## Key Entities

- **ExportArtifact**: PDF or social preview and readiness state.
- **NativeShareBoundary**: Share sheet target and non-transmission default.
- **WatchSendRequest**: Workout, device state, and transfer result.
- **ExternalIntegrationProvider**: Provider metadata and auth state.

## Success Criteria

- **SC-001**: Preview and native share target selection are separate states.
- **SC-002**: Watch send can fail safely without losing workout context.
- **SC-003**: Legal/review/subscription leaves can be exited without app state mutation.

## Assumptions

- External SDK wiring belongs to implementation planning and may use stubs first.
- PDF renderer quality can be improved after route contracts are stable.
