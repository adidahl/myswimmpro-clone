# Research: App Shell and Navigation Foundation

## Decision: Use Expo SDK 55 default template

**Rationale**: The current Expo documentation available through Context7 exposes
SDK 55 as the latest SDK branch and documents creating a router-enabled app with
`npx create-expo-app@latest --template default@sdk-55`. This gives us a known
Expo Router setup, TypeScript-ready structure, Android/iOS/web support, and a
path the user already knows.

**Alternatives considered**:
- Bare React Native: more native control, but slower setup and unnecessary for
  a shell-first clone.
- Existing web-only React app: faster browser iteration, but weaker alignment
  with native app navigation, native leaves, and mobile route behavior.
- Expo SDK 54: stable previous branch, but less current than SDK 55.

## Decision: Use Expo Router for navigation

**Rationale**: Expo Router provides file-based routing, root Stack layouts,
route groups, native/web support, modal presentation options, not-found routes,
and native intent rewrite hooks. The shell spec needs bottom tabs, nested stack
routes, modal/sheet hosts, and safe native boundaries; Expo Router maps directly
to those needs.

**Alternatives considered**:
- Manually configured React Navigation only: powerful but adds more custom route
  registry work before the app has feature code.
- A custom router abstraction: violates the constitution's reuse/simplicity
  intent and risks divergence from Expo conventions.

## Decision: Root Stack with `(tabs)` route group

**Rationale**: Expo docs show a root `Stack` whose `(tabs)` screen hides the
header. This matches the app shell: tabs own the primary surface while stack
routes and modal routes sit above them.

**Alternatives considered**:
- Put every route inside a tab group: simpler at first, but modal/native/shared
  routes would become awkward and could lose source tab context.
- Separate root stacks per tab only: may be useful later, but the first shell
  can preserve origin context through typed route metadata.

## Decision: Use modal presentation routes for shell overlays

**Rationale**: Expo Router supports modal and transparent modal presentations
through `Stack.Screen` options. Start Menu and import choices are shell-owned
overlay hosts in this feature; representing them as routes keeps back/close
behavior testable.

**Alternatives considered**:
- Component-local state only: harder to deep link or test as route contracts.
- Native action sheets only: too final and platform-specific for the first
  cross-platform shell contract.

## Decision: Use `+native-intent.tsx` for defensive native path rewrites

**Rationale**: Expo docs describe `redirectSystemPath` for incoming native deep
links and explicitly note it must not crash on malformed paths. This feature
requires safe native/external boundaries and unsupported route handling.

**Alternatives considered**:
- Ignore native intents until integration specs: would leave a known shell gap.
- Let each integration own its own incoming route handling: risks duplicate
  boundary handling and inconsistent error states.

## Decision: Route tests with Expo Router `renderRouter`

**Rationale**: Expo Router includes test guidance for rendering route maps and
asserting pathname changes. The shell can validate tab, stack, modal, and risky
boundary contracts before feature business logic exists.

**Alternatives considered**:
- Only manual smoke testing: insufficient for route contracts that later agents
  will depend on.
- Full E2E first: valuable later, but too heavy before the app shell exists.

## Sources Consulted

- Context7 Expo docs for `/expo/expo/__branch__sdk-55`.
- Expo Router docs excerpts for root `Stack`, `(tabs)` group, modal
  presentation, `+native-intent.tsx`, create-expo-app SDK template, and
  `renderRouter` route tests.
