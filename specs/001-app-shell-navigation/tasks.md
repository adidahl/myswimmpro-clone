# Tasks: App Shell and Navigation Foundation

**Input**: Design documents from `specs/001-app-shell-navigation/`

**Prerequisites**: spec.md, plan.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: Included because the plan requires route contract validation before implementation.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (US1, US2, US3)
- Every task includes an exact file path or command target

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Create the Expo SDK 55 TypeScript app foundation without implementing feature-specific business logic.

- [ ] T001 Scaffold Expo SDK 55 template in `.tmp/expo-template` using `npx create-expo-app@latest .tmp/expo-template --template default@sdk-55` and merge app scaffold into repository root without deleting `specs/`, `.specify/`, `.agents/`, `APP_ARCHITECTURE.md`, or `manual-navigation-map/`
- [ ] T002 Configure npm scripts `typecheck`, `lint`, `test`, and `start:web` in `package.json`
- [ ] T003 Configure TypeScript strict project checks in `tsconfig.json`
- [ ] T004 Configure Jest/React Native Testing Library setup in `jest.config.js`
- [ ] T005 [P] Create test setup file in `src/test-utils/setupTests.ts`
- [ ] T006 [P] Create shared router test helper in `src/test-utils/renderRouter.tsx`
- [ ] T007 [P] Add placeholder image/icon asset directory in `assets/images/`

**Checkpoint**: Expo app can install dependencies and expose validation scripts.

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Define shared navigation contracts, shell state, and placeholder primitives required by all user stories.

**Critical**: No user story work starts until this phase is complete.

- [ ] T008 Create primary tab registry in `src/navigation/appTabs.ts`
- [ ] T009 Create route ownership map in `src/navigation/routeOwnership.ts`
- [ ] T010 Create route registry from `contracts/route-contract.md` in `src/navigation/routeRegistry.ts`
- [ ] T011 Create risky action registry from `contracts/native-boundary-contract.md` in `src/navigation/riskyActions.ts`
- [ ] T012 [P] Create navigation fixture states in `src/navigation/navigationFixtures.ts`
- [ ] T013 [P] Create shared placeholder component in `src/components/PlaceholderSurface.tsx`
- [ ] T014 [P] Create safe boundary notice component in `src/components/SafeBoundaryNotice.tsx`
- [ ] T015 [P] Create shell header component in `src/components/AppShellHeader.tsx`
- [ ] T016 [P] Create primary tab icon component in `src/components/PrimaryTabIcon.tsx`
- [ ] T017 Add route registry contract tests in `__tests__/contracts/route-registry.test.ts`

**Checkpoint**: Shared route and safety contracts are typed and testable.

## Phase 3: User Story 1 - Navigate Primary Tabs (Priority: P1)

**Goal**: Home, Library, Trends, and Profile tabs are reachable with correct active tab state and placeholder content.

**Source Evidence**: APP_ARCHITECTURE.md Root Navigation and Home/Library/Trends/Profile routes; NAVIGATION.md S001, S115, S116, S117, S176, S180, S181, S247-S250.

**Independent Test**: Starting from Home, visit Library, Trends, Profile, and Home again while preserving active tab state.

### Tests for User Story 1

- [ ] T018 [P] [US1] Add primary tab navigation tests in `__tests__/navigation/primary-tabs.test.tsx`
- [ ] T019 [P] [US1] Add post-log tab return fixture tests in `__tests__/navigation/post-log-tabs.test.tsx`

### Implementation for User Story 1

- [ ] T020 [US1] Implement root Stack layout with `(tabs)` group in `app/_layout.tsx`
- [ ] T021 [US1] Implement tab layout with Home, Library, Trends, Profile in `app/(tabs)/_layout.tsx`
- [ ] T022 [P] [US1] Implement Home placeholder route in `app/(tabs)/index.tsx`
- [ ] T023 [P] [US1] Implement Library placeholder route in `app/(tabs)/library.tsx`
- [ ] T024 [P] [US1] Implement Trends placeholder route in `app/(tabs)/trends.tsx`
- [ ] T025 [P] [US1] Implement Profile placeholder route in `app/(tabs)/profile.tsx`
- [ ] T026 [US1] Wire tab labels, active state, and source evidence copy using `src/navigation/appTabs.ts`
- [ ] T027 [US1] Validate US1 with `npm test -- __tests__/navigation/primary-tabs.test.tsx`

**Checkpoint**: User Story 1 works independently as the MVP shell.

## Phase 4: User Story 2 - Open and Return From Shared Shell Routes (Priority: P2)

**Goal**: Representative shared stack routes, modal/sheet routes, Support, Coach Chat, and placeholders preserve origin context and return behavior.

**Source Evidence**: APP_ARCHITECTURE.md Shared Workout Routes, Support Routes, Start Menu Pattern; NAVIGATION.md S007, S008, S010, S021, S022, S033, S067, S075, S149, S150.

**Independent Test**: Open shared routes from Home/Library, close/back out, and confirm the origin route and tab are restored.

### Tests for User Story 2

- [ ] T028 [P] [US2] Add shared stack route tests in `__tests__/navigation/shared-routes.test.tsx`
- [ ] T029 [P] [US2] Add modal route return tests in `__tests__/navigation/modal-routes.test.tsx`
- [ ] T030 [P] [US2] Add support route return tests in `__tests__/navigation/support-routes.test.tsx`

### Implementation for User Story 2

- [ ] T031 [US2] Implement workout placeholder stack route in `app/workout/[workoutId].tsx`
- [ ] T032 [US2] Implement Start Menu modal placeholder in `app/modal/start-menu.tsx`
- [ ] T033 [US2] Implement Import Workout modal placeholder in `app/modal/import-workout.tsx`
- [ ] T034 [US2] Implement Support root placeholder in `app/support/index.tsx`
- [ ] T035 [US2] Implement Support messages placeholder in `app/support/messages.tsx`
- [ ] T036 [US2] Implement Coach Chat scoped placeholder in `app/coach-chat/[scopeType]/[scopeId].tsx`
- [ ] T037 [US2] Add not-found route and safe Home return in `app/+not-found.tsx`
- [ ] T038 [US2] Wire shared route actions through `src/navigation/routeRegistry.ts`
- [ ] T039 [US2] Validate US2 with `npm test -- __tests__/navigation/shared-routes.test.tsx`

**Checkpoint**: User Stories 1 and 2 both work independently.

## Phase 5: User Story 3 - Guard Risky and Native Boundary Actions (Priority: P3)

**Goal**: Native, external, destructive, account-changing, and transmitting actions are represented as safe boundaries without final execution.

**Source Evidence**: APP_ARCHITECTURE.md Risky / Final Actions and Native/external leaves; NAVIGATION.md S019, S022, S075-S080, S114, S121-S124, S129-S131, S227-S233.

**Independent Test**: Open representative native/risky boundaries and confirm no action transmits, mutates account data, or selects native targets.

### Tests for User Story 3

- [ ] T040 [P] [US3] Add native boundary route tests in `__tests__/navigation/native-boundaries.test.tsx`
- [ ] T041 [P] [US3] Add risky action gate tests in `__tests__/navigation/risky-actions.test.tsx`

### Implementation for User Story 3

- [ ] T042 [US3] Implement generic native boundary placeholder in `app/native-boundary/[boundaryType].tsx`
- [ ] T043 [US3] Implement defensive native intent rewrite in `app/+native-intent.tsx`
- [ ] T044 [US3] Wire boundary metadata through `src/navigation/riskyActions.ts`
- [ ] T045 [US3] Add safe boundary UI copy through `src/components/SafeBoundaryNotice.tsx`
- [ ] T046 [US3] Validate US3 with `npm test -- __tests__/navigation/native-boundaries.test.tsx`

**Checkpoint**: All shell-owned risky/native boundaries are non-executing and testable.

## Phase 6: Polish and Cross-Cutting Concerns

**Purpose**: Validate evidence traceability, quickstart, and shell readiness before later feature packages consume it.

- [ ] T047 [P] Add route evidence comments or metadata references for S001, S115, S116, S117, S149, S176, S181, and S247-S250 in `src/navigation/routeRegistry.ts`
- [ ] T048 [P] Add README usage notes for the app shell in `README.md`
- [ ] T049 Run `npm run typecheck`
- [ ] T050 Run `npm run lint`
- [ ] T051 Run `npm test`
- [ ] T052 Run quickstart manual smoke checks from `specs/001-app-shell-navigation/quickstart.md`
- [ ] T053 Audit shared route ownership against `specs/README.md`
- [ ] T054 Audit risky/final action gates against `specs/001-app-shell-navigation/contracts/native-boundary-contract.md`

## Dependencies and Execution Order

### Phase Dependencies

- Phase 1 Setup has no dependencies.
- Phase 2 Foundational depends on Phase 1.
- User Story phases depend on Phase 2.
- US1 is the MVP and should complete before US2/US3 implementation begins.
- US2 depends on US1 for tab origin behavior.
- US3 depends on US2 route placeholders for origin/return coverage.
- Polish depends on selected user story phases.

### Parallel Opportunities

- T005-T007 can run in parallel after T004.
- T012-T016 can run in parallel after T008-T011 are defined.
- T018 and T019 can run in parallel.
- T022-T025 can run in parallel after T021.
- T028-T030 can run in parallel.
- T034-T036 can run in parallel after route registry entries exist.
- T040 and T041 can run in parallel.
- T047 and T048 can run in parallel.

## Implementation Strategy

### MVP First

1. Complete Phase 1.
2. Complete Phase 2.
3. Complete Phase 3 for US1.
4. Stop and validate the four-tab shell before adding shared routes.

### Incremental Delivery

1. US1: Primary tabs and top-level placeholders.
2. US2: Shared stack/modal/support route hosts.
3. US3: Native/risky boundary handling.
4. Polish: Evidence audit, quickstart, full validation commands.

### Agent Handoff Notes

- Do not implement feature-specific business logic inside shell placeholders.
- Keep route contracts stable for later specs 002-018.
- Do not execute final native/external actions in this feature.
- Preserve exact task IDs in commit messages or implementation notes.
