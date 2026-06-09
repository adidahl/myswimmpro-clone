# Feature Specification: App Shell and Navigation Foundation

**Feature Branch**: `001-app-shell-navigation`

**Created**: 2026-06-09

**Status**: Draft

**Input**: User description: "Build the App Shell and Navigation foundation for the swim training app. Use APP_ARCHITECTURE.md as the source architecture. Scope includes authenticated app container, bottom tabs, shared headers, stack routing, modal/sheet host, native-intent bridge stubs, support entry points, and navigation return behavior. Reference screen cluster S001-S150, S176-S181, S247-S250 from manual-navigation-map/NAVIGATION.md. Do not implement feature-specific workout, plan, trend, or profile business logic beyond placeholders required for navigation validation."

## Architecture Evidence *(mandatory)*

- **Architecture source**: APP_ARCHITECTURE.md Product Shape, High-Level System Architecture, Frontend Feature Modules, Route / Screen Inventory, Shared Interaction Patterns, Risky / Final Actions, Suggested Agent Work Packages, MVP Sequencing, PRD Checklist, and Source Screen Clusters.
- **Suggested work package**: Work package 1, "App shell and navigation: bottom tabs, stack routing, modal/sheet host, native bridge stubs."
- **Source screen clusters**: Home/create flows S001-S089; Generated workout/shared detail/actions S007-S035; Custom workout editor/actions S036-S066; Saved workout library S067-S074 and S152-S153; Image import S075-S080; Training plan generation/detail/workout S081-S114; Bottom tabs/profile/settings S115-S150, S176-S181, S247-S250.
- **Referenced screens**: Key evidence includes S001_home, S007_generated_workout_result, S008_start_workout_menu, S021_workout_pdf, S022_pdf_share_sheet, S033_coach_chat_result, S067_swim_workout_library, S075_import_workout_from_image_result, S081_create_training_plan_result, S115_library_tab, S116_trends_tab, S117_profile_tab, S118_profile_settings, S149_home_support_result, S176_trends_tab_return_result, S181_library_from_profile_result, and S247-S250 post-log bottom-tab returns. Local evidence lives under manual-navigation-map/screenshots/ and manual-navigation-map/states/.
- **Explicitly out of scope**: Workout generation logic, custom workout editing behavior, activity logging persistence, PDF rendering, Coach Chat messaging, support article content, account/device/privacy/legal implementation, training plan generation, analytics calculations, profile data editing, and real native share/photo/camera transmission.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Navigate Primary Tabs (Priority: P1)

As an authenticated swimmer, I can move between Home, Library, Trends, and Profile using the bottom tabs while each tab presents the correct top-level shell and preserves clear return behavior.

**Why this priority**: The bottom-tab shell is the foundation for every later feature package. Without it, deeper routes cannot be validated against the mapped product.

**Independent Test**: Starting from Home, visit Library, Trends, Profile, and return to Home using only primary tab navigation. Confirm each tab has the expected shell, active tab state, and source-screen-compatible placeholder content.

**Acceptance Scenarios**:

1. **Given** the authenticated app shell is open on Home, **When** the user selects Library, **Then** the shell shows Library as the active tab and presents a Library placeholder matching the mapped tab role.
2. **Given** the authenticated app shell is open on Library, **When** the user selects Trends, **Then** the shell shows Trends as the active tab and presents a Trends placeholder matching the mapped tab role.
3. **Given** the authenticated app shell is open on Trends, **When** the user selects Profile, **Then** the shell shows Profile as the active tab and presents a Profile placeholder matching the mapped tab role.
4. **Given** the authenticated app shell is open after a completed workout state, **When** the user selects Library, Trends, Profile, and Home, **Then** the shell preserves the post-log tab-return behavior represented by S247-S250.

---

### User Story 2 - Open and Return From Shared Shell Routes (Priority: P2)

As a swimmer exploring top-level actions, I can enter shared routed surfaces such as workout detail placeholders, support entry points, modal/sheet hosts, and native-intent leaves, then return to the correct prior context without losing tab state.

**Why this priority**: Most product flows reuse the same route and modal patterns. Establishing the host behavior early prevents later feature packages from inventing incompatible navigation.

**Independent Test**: From Home and Library placeholders, open representative stack routes, modal/sheet routes, and native-intent leaves; then close or go back and confirm the prior tab and route context are restored.

**Acceptance Scenarios**:

1. **Given** Home is active, **When** the user opens a representative workout detail route and navigates back, **Then** the shell returns to Home without changing the active tab.
2. **Given** a workout detail placeholder is open, **When** the user opens the Start Menu host and closes it, **Then** the underlying workout detail route remains visible and unchanged.
3. **Given** a PDF or share leaf is opened from a workout placeholder, **When** the user backs out, **Then** the shell returns through the PDF placeholder to the originating workout placeholder.
4. **Given** a Support entry point is opened from any primary tab, **When** the user closes Support, **Then** the shell returns to the originating tab.

---

### User Story 3 - Guard Risky and Native Boundary Actions (Priority: P3)

As a swimmer, I can see navigation boundaries for risky, external, or native actions without accidentally deleting data, logging out, sending messages, selecting share targets, or transmitting content.

**Why this priority**: The navigation evidence contains many final or native leaves. The shell must model them safely before feature agents add real behavior.

**Independent Test**: Open representative risky or native boundary actions and confirm they are either blocked as non-transmitting leaves, require explicit confirmation, or return safely without performing the final action.

**Acceptance Scenarios**:

1. **Given** a share sheet placeholder is visible, **When** the user backs out without choosing a target, **Then** no transmission occurs and the shell returns to the prior in-app surface.
2. **Given** a destructive action such as delete, cancel, logout, or account deletion is requested, **When** the shell handles the route, **Then** it presents a confirmation-gated or blocked placeholder rather than executing the action.
3. **Given** a Coach Chat or support message surface is opened, **When** the user has not explicitly sent a message, **Then** the route can close without creating or transmitting a message.

### Edge Cases

- Unknown or unsupported route paths return to a safe top-level tab or a not-found shell state without crashing.
- Back navigation from a top-level tab does not skip across unrelated tab histories.
- Modal/sheet close actions and system back actions produce the same return state when the source evidence shows equivalent behavior.
- Native photo, camera, share, review, subscription, and legal leaves are represented as safe placeholders unless a later feature spec explicitly owns the final handoff.
- Loading, empty, error, permission denied, offline, and navigation return states are defined for shell-owned routes and placeholder content where applicable.
- Risky/final actions are confirmation-gated or modeled as blocked leaf actions.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The system MUST provide an authenticated app shell with four primary tabs: Home, Library, Trends, and Profile.
- **FR-002**: The system MUST show the active primary tab consistently while moving between top-level tabs.
- **FR-003**: The system MUST provide stack routing for deeper app routes without losing the originating tab context.
- **FR-004**: The system MUST provide a modal/sheet host for shared overlay patterns such as Start Menu and import choices.
- **FR-005**: The system MUST provide native-intent boundary placeholders for share, photo library, camera, review, subscription, legal, and support handoffs.
- **FR-006**: The system MUST provide shared header behavior for route title, navigate-up, close, and overflow controls where those controls appear in source evidence.
- **FR-007**: The system MUST support Support entry points from Home, Library, Trends, Profile, and Settings placeholders, returning to the originating context on close.
- **FR-008**: The system MUST preserve bottom-tab return behavior for the post-log state represented by S247-S250.
- **FR-009**: The system MUST expose placeholder route targets for later feature packages without implementing their business logic.
- **FR-010**: The system MUST prevent unsupported routes and malformed route parameters from breaking the shell.

### State, Navigation, and Safety Requirements

- **SR-001**: The system MUST define loading, empty, success, error, permission denied, offline, and navigation return states where applicable.
- **SR-002**: The system MUST preserve shared action contracts from APP_ARCHITECTURE.md for reused surfaces.
- **SR-003**: The system MUST identify risky/final actions and required confirmation or leaf behavior.
- **SR-004**: The system MUST not transmit content, send messages, change account data, delete data, or connect integrations from shell placeholders.
- **SR-005**: The system MUST record route ownership boundaries so later feature packages can replace placeholders without changing shell contracts.

### Key Entities *(include if feature involves data)*

- **AppTab**: A primary navigation destination: Home, Library, Trends, or Profile.
- **RouteEntry**: A navigable path, parameters, source tab, title behavior, and return behavior.
- **OverlayState**: A modal or sheet presentation with origin route, close behavior, and allowed actions.
- **NativeIntentBoundary**: A safe representation of a native or external handoff, including origin route and non-transmission default behavior.
- **RiskyActionGate**: A confirmation or blocked-leaf model for destructive, account-changing, transmitting, or final actions.
- **PlaceholderSurface**: A shell-owned stand-in for feature routes whose business logic belongs to later work packages.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: A reviewer can navigate Home, Library, Trends, Profile, and back to Home in under 60 seconds while seeing the correct active tab after each action.
- **SC-002**: 100% of shell-owned routes listed for this feature have documented return behavior.
- **SC-003**: 100% of risky/final actions in this feature are blocked, confirmation-gated, or represented as non-transmitting leaves.
- **SC-004**: At least one representative stack route, one modal/sheet route, one support route, and one native-intent boundary can be validated independently.
- **SC-005**: Later feature packages can attach to placeholder route targets without changing the primary tab contract.

## Assumptions

- Authentication/session creation is provided outside this feature; the shell starts in an authenticated state.
- Placeholder content is acceptable when it preserves route contracts and source-screen roles.
- Feature-specific data fetching and persistence are deferred to later work packages.
- Native share/photo/camera/review/subscription/legal handoffs remain non-transmitting placeholders in this feature.
- The first implementation target will be chosen during planning and must respect the shell contracts above.
