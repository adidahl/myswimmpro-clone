# Feature Specification: Import Workout From Image

**Feature Branch**: `006-image-import-workout`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 6 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Workout Creation Routes, Image Import Service, Async Jobs.
- **Source screen clusters**: S075-S080.
- **Referenced screens**: S075, S076, S077, S078, S079, S080.
- **Explicitly out of scope**: OCR accuracy tuning, real camera/photo upload, generated workout logic, library persistence.

## User Scenarios & Testing

### User Story 1 - Choose Import Source (Priority: P1)

As a swimmer, I can open Import Workout and choose Photo Library or Camera.

**Independent Test**: Open the import dialog and confirm both choices are visible and cancellable.

### User Story 2 - Enter Native Media Boundary (Priority: P2)

As a swimmer, I can enter photo library or camera boundary safely and return without selecting or uploading media.

**Independent Test**: Open each native boundary placeholder and back out to the originating app context.

### User Story 3 - Normalize Imported Workout (Priority: P3)

As a swimmer, after selecting an image in a later implementation, I can review extracted workout content before saving or starting it.

**Independent Test**: Use a fixture import result and confirm it routes to a reviewable Workout Detail or editor surface.

## Requirements

- **FR-001**: The system MUST present Import from Photo Library and Import from Camera choices.
- **FR-002**: Native media boundaries MUST not upload or transmit content without explicit selection and confirmation.
- **FR-003**: Import cancellation MUST return to the source screen without changing app state.
- **FR-004**: OCR/extraction output MUST normalize into the shared Workout model before review.
- **SR-001**: Permission denied, no media, camera unavailable, extraction failure, and offline states MUST be defined.
- **SR-002**: Image selection and upload are final/native actions and MUST be gated by the owning implementation.

## Key Entities

- **ImageImportRequest**: Source type, selected media metadata, and permission state.
- **ImportExtractionJob**: Async OCR/extraction lifecycle.
- **ImportedWorkoutDraft**: Reviewable workout candidate from extraction.

## Success Criteria

- **SC-001**: Photo and camera boundaries can be opened and exited without transmission.
- **SC-002**: Fixture extraction output can become a reviewable workout.
- **SC-003**: Permission-denied behavior is specified before implementation.

## Assumptions

- Native media integration can be stubbed until platform setup is complete.
- OCR processing is asynchronous and may fail.
