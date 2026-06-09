# Feature Specification: Support and Coach Chat

**Feature Branch**: `016-support-coach-chat`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 16 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Support Routes, Coach Service, Support Service, Shared surfaces.
- **Source screen clusters**: S033-S034, S064-S065, S110-S111, S140-S141, S149-S150, S174-S178, S202-S221, S238-S239.
- **Referenced screens**: S033, S064, S110, S140, S149, S203, S204, S206, S238.
- **Explicitly out of scope**: Deep support article content authoring, actual message transmission without explicit send.

## User Scenarios & Testing

### User Story 1 - Open Support From App Surfaces (Priority: P1)

As a swimmer, I can open Support from Home, Library, Trends, Profile, or Settings and close back to the origin.

**Independent Test**: Open Support from multiple origins and confirm return routes.

### User Story 2 - Browse Help Center Lightly (Priority: P2)

As a swimmer, I can browse collections and articles without leaving the app unexpectedly.

**Independent Test**: Open one collection and one article, then back to support root.

### User Story 3 - Open Scoped Coach Chat (Priority: P3)

As a swimmer, I can open Coach Chat scoped to a workout or completed activity and close it without sending a message.

**Independent Test**: Open scoped Coach Chat from workout and completed detail placeholders and back out.

## Requirements

- **FR-001**: Support root MUST expose Help, Messages, article cards, and close.
- **FR-002**: Help center MUST support collection and article routes where included in scope.
- **FR-003**: Coach Chat MUST be scope-aware for workout or completed activity context.
- **FR-004**: Message send MUST require explicit user action and must not happen on route open/close.
- **SR-001**: Support article depth is low priority unless a feature explicitly depends on content.
- **SR-002**: Offline, unavailable support provider, empty message, send failure, and back-return states MUST be defined.

## Key Entities

- **SupportEntryContext**: Origin tab/route and return target.
- **SupportArticle**: Collection/article metadata.
- **CoachThread**: Scope type, scope ID, messages, and permissions.
- **CoachMessageDraft**: Unsaved outbound message state.

## Success Criteria

- **SC-001**: Support can open and close from at least four origins.
- **SC-002**: Coach Chat opens with visible scope notice and no auto-send.
- **SC-003**: Help navigation return paths are documented.

## Assumptions

- Support may be first-party or bridged to an external provider.
- Article content itself is not a blocker for MVP app navigation.
