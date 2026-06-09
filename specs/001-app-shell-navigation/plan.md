# Implementation Plan: App Shell and Navigation Foundation

**Branch**: `001-app-shell-navigation` | **Date**: 2026-06-09 | **Spec**: specs/001-app-shell-navigation/spec.md

**Input**: Feature specification from `specs/001-app-shell-navigation/spec.md`

## Summary

Build the first executable app foundation as an Expo SDK 55 React Native and
TypeScript application using Expo Router. Because this repository already
contains planning evidence, implementation should create an SDK 55 template in a
temporary directory and merge the app scaffold into the repository root. The
feature delivers an authenticated app shell with Home, Library, Trends, and
Profile tabs, stack routing for shared placeholder surfaces, modal/sheet hosts,
safe native-intent boundaries, and evidence-backed route return behavior.
Feature-specific business logic remains stubbed behind typed placeholder
contracts.

## Technical Context

**Language/Version**: TypeScript with Expo SDK 55 default template.

**Primary Dependencies**: Expo, Expo Router, React Native, React, Jest or Expo
test runner setup, @testing-library/react-native, expo-router test utilities.

**Storage**: No durable storage for this feature. Route fixtures and shell state
are local in source files.

**Testing**: TypeScript typecheck, linting, unit/integration route tests with
Expo Router `renderRouter`, and manual Expo web/mobile smoke checks.

**Target Platform**: Expo Android, iOS, and web. The visual validation priority
for this first feature is web plus one mobile viewport; native parity is covered
by route contracts and later emulator testing.

**Project Type**: Mobile app with web-capable Expo Router shell.

**Performance Goals**: Primary tab switches and placeholder route transitions
should feel immediate to a reviewer; no route transition may require remote data
for this feature.

**Constraints**: No final native transmission, account mutation, message send,
delete, logout, integration connection, or share target selection. Shared route
contracts must remain replaceable by later feature packages.

**Scale/Scope**: One root Expo app, four primary tabs, representative stack
routes, representative modal/sheet routes, representative native boundaries,
and typed contracts for later feature ownership.

## Architecture Evidence

**Architecture Source**: APP_ARCHITECTURE.md Product Shape, Frontend Feature
Modules, Route / Screen Inventory, Shared Interaction Patterns, Risky / Final
Actions, Suggested Agent Work Packages, MVP Sequencing, PRD Checklist, and
Source Screen Clusters.

**Navigation Evidence**: manual-navigation-map/NAVIGATION.md with primary
evidence from S001, S007, S008, S021, S022, S033, S067, S075, S081, S115,
S116, S117, S118, S149, S176, S181, and S247-S250.

**Shared Surfaces Reused**: Workout Detail placeholder, Start Menu placeholder,
PDF/share placeholder, Support placeholder, Coach Chat placeholder, image import
placeholder, training plan placeholder, settings placeholder.

**Risky/Final Actions**: Native share target selection, camera/photo selection,
message send, delete, logout, account deletion, subscription management,
diagnostic logs, integration toggles, app review, and legal handoff are modeled
as safe boundaries or confirmation-gated placeholders.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- Evidence-Backed Product Scope: PASS. Spec cites APP_ARCHITECTURE.md and
  manual-navigation-map screen clusters with explicit out-of-scope behavior.
- Shared Flow and Domain Reuse: PASS. Shared route hosts are shell-owned
  placeholders with later feature ownership documented in contracts.
- Pre-Implementation Analysis Gates: PASS. Spec and checklist exist; this plan
  will generate research, data model, contracts, quickstart, tasks, and analysis
  before implementation.
- Traceable Validation: PASS. User stories map to source evidence, route
  contracts, tasks, and quickstart validation.
- Risky Action and Privacy Safety: PASS. Final/native actions are non-executing
  boundaries until owning specs replace them.

## Project Structure

### Documentation (this feature)

```text
specs/001-app-shell-navigation/
├── spec.md
├── checklists/
│   └── requirements.md
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   ├── route-contract.md
│   ├── shell-state-contract.md
│   └── native-boundary-contract.md
└── tasks.md
```

### Source Code (repository root)

```text
app/
├── _layout.tsx
├── +not-found.tsx
├── +native-intent.tsx
├── (tabs)/
│   ├── _layout.tsx
│   ├── index.tsx
│   ├── library.tsx
│   ├── trends.tsx
│   └── profile.tsx
├── workout/
│   └── [workoutId].tsx
├── support/
│   ├── index.tsx
│   └── messages.tsx
├── coach-chat/
│   └── [scopeType]/
│       └── [scopeId].tsx
├── native-boundary/
│   └── [boundaryType].tsx
└── modal/
    ├── start-menu.tsx
    └── import-workout.tsx

src/
├── navigation/
│   ├── appTabs.ts
│   ├── routeRegistry.ts
│   ├── routeOwnership.ts
│   ├── riskyActions.ts
│   └── navigationFixtures.ts
├── components/
│   ├── AppShellHeader.tsx
│   ├── PlaceholderSurface.tsx
│   ├── PrimaryTabIcon.tsx
│   └── SafeBoundaryNotice.tsx
└── test-utils/
    └── renderRouter.tsx

__tests__/
├── navigation/
│   ├── primary-tabs.test.tsx
│   ├── shared-routes.test.tsx
│   └── native-boundaries.test.tsx
└── contracts/
    └── route-registry.test.ts

assets/
└── images/
```

**Structure Decision**: Use Expo Router's `app/` directory at repository root
with route groups for tabs, explicit stack routes for placeholders, and
co-located typed route contracts in `src/navigation/`. This follows Expo SDK 55
Router guidance for root Stack plus `(tabs)` and keeps shell-owned contracts
replaceable by later feature packages.

## Validation Strategy

**Independent Story Validation**:
- US1: Route tests verify Home, Library, Trends, Profile navigation and active
  tab state.
- US2: Route tests verify stack placeholder, modal placeholder, PDF/share
  placeholder, Support placeholder, and return behavior.
- US3: Route tests verify native/risky boundaries do not execute final actions.

**State Coverage**: Loading, empty, success, error, permission denied, offline,
not-found, and back/return states are represented as typed shell states and
fixture routes.

**Evidence Checks**: Quickstart references S001, S115, S116, S117, S149, S176,
S181, and S247-S250 for manual smoke validation.

## Complexity Tracking

No constitution violations.

## Phase 0: Research Summary

Research decisions are captured in `research.md`. Main decisions:
- Use Expo SDK 55 default template.
- Use Expo Router root `Stack` plus `(tabs)` group.
- Use modal presentation routes for shell-owned overlays.
- Use `+native-intent.tsx` for defensive native deep-link handling.
- Use Expo Router `renderRouter` and React Native Testing Library for route
  contract tests.

## Phase 1: Design Summary

Design details are captured in:
- `data-model.md` for shell entities and validation rules.
- `contracts/route-contract.md` for route registry, ownership, and return
  behavior.
- `contracts/shell-state-contract.md` for tab, route, overlay, and placeholder
  states.
- `contracts/native-boundary-contract.md` for non-transmitting native/external
  boundaries.
- `quickstart.md` for validation commands and manual evidence checks.

## Post-Design Constitution Check

- Evidence-Backed Product Scope: PASS. Contracts reference source screen IDs.
- Shared Flow and Domain Reuse: PASS. Shared surfaces are represented once in
  route registry and placeholder components.
- Pre-Implementation Analysis Gates: PASS. `tasks.md` and `analysis.md` are
  generated before implementation.
- Traceable Validation: PASS. Tasks will reference story IDs, file paths, and
  validation commands.
- Risky Action and Privacy Safety: PASS. Native boundary contract forbids
  final action execution in this feature.
