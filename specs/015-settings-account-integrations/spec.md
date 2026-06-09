# Feature Specification: Settings, Account, Devices, Privacy, and Legal

**Feature Branch**: `015-settings-account-integrations`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 15 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Settings Routes, Risky / Final Actions, Auth/Account Service, Device Integration Service, Legal/Compliance Service.
- **Source screen clusters**: S118-S132, plus settings support S125-S126.
- **Referenced screens**: S118, S119, S121, S123, S127, S129, S131.
- **Explicitly out of scope**: Real billing portal execution, real integration token exchange, destructive account actions without confirmation.

## User Scenarios & Testing

### User Story 1 - Navigate Settings (Priority: P1)

As a swimmer, I can open Settings and reach Account, Devices, Share App, Support, Privacy, and Terms leaves.

**Independent Test**: Open each settings route and return to Settings/Profile context.

### User Story 2 - Manage Account and Privacy Safely (Priority: P2)

As a swimmer, I can view account and privacy options without accidentally logging out, deleting data, or changing tracking settings.

**Independent Test**: Open risky account/privacy actions and confirm they are confirmation-gated or blocked placeholders.

### User Story 3 - View Devices and Legal Boundaries (Priority: P3)

As a swimmer, I can view integration options and legal WebView placeholders safely.

**Independent Test**: Open device/legal routes and back out without external account mutation.

## Requirements

- **FR-001**: Settings MUST list Account Settings, Devices & Integrations, Share App, Support, Send Logs, Write Review, Privacy, and Terms.
- **FR-002**: Account Settings MUST expose email, name/picture edit, private activity, subscription management, logout, and related placeholders.
- **FR-003**: Devices MUST expose Strava, Garmin, Health Connect, TrainingPeaks, and authorization-code entry placeholders.
- **FR-004**: Privacy MUST expose tracking limit, privacy policy, download account data, and delete account placeholders.
- **FR-005**: Terms MUST open legal WebView or external legal placeholder.
- **SR-001**: Logout, delete account, data export, diagnostic logs, integration toggles, review, and subscription actions MUST be confirmation-gated or external leaves.
- **SR-002**: Permission denied, offline, external failure, cancelled leaf, and return states MUST be defined.

## Key Entities

- **SettingsRoute**: Settings item and target.
- **AccountSettingsState**: Account profile, privacy, subscription, logout options.
- **IntegrationConnection**: Provider connection and authorization state.
- **LegalDocumentLink**: Legal URL/WebView target and return route.

## Success Criteria

- **SC-001**: Every Settings item has a route target or explicit blocked placeholder.
- **SC-002**: Destructive/account-changing actions cannot execute without confirmation.
- **SC-003**: Legal and native leaves can be exited safely.

## Assumptions

- Real provider OAuth and billing flows belong to integration implementation phases.
- Initial settings can be mostly view-only placeholders.
