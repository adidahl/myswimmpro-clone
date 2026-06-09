# Data Model: App Shell and Navigation Foundation

## Entity: AppTab

Represents one primary bottom-tab destination.

Fields:
- `id`: one of `home`, `library`, `trends`, `profile`.
- `label`: display label.
- `route`: Expo Router pathname for the tab.
- `sourceScreens`: evidence screen IDs.
- `isPrimary`: always true for these four tabs.

Validation:
- `id` must be unique.
- `route` must map to a file under `app/(tabs)/`.
- Every AppTab must have at least one source screen reference.

## Entity: RouteEntry

Represents a shell-owned route or placeholder route.

Fields:
- `id`: stable route identifier.
- `pathname`: Expo Router pathname pattern.
- `owner`: owning feature spec ID.
- `originTab`: optional AppTab ID for default return behavior.
- `presentation`: `tab`, `stack`, `modal`, `native-boundary`, or `not-found`.
- `title`: optional header title.
- `sourceScreens`: source evidence screen IDs.
- `allowedActions`: route-local action IDs.
- `returnBehavior`: expected close/back target.

Validation:
- `pathname` must be unique.
- `owner` must reference a spec in `specs/README.md`.
- `presentation` determines required return behavior.
- `native-boundary` routes must also have a NativeIntentBoundary.

## Entity: OverlayState

Represents shell-owned modal or sheet presentation.

Fields:
- `id`: stable overlay identifier.
- `route`: modal route pathname.
- `originRoute`: route that opened the overlay.
- `dismissAction`: `close`, `back`, or both.
- `underlyingRouteRemainsVisible`: boolean.
- `allowedActions`: overlay actions and owning routes.

Validation:
- `originRoute` must exist as RouteEntry.
- Every overlay action must be either shell-owned or delegated to a later spec.
- Dismissal must not mutate business data.

## Entity: NativeIntentBoundary

Represents a native or external handoff that this feature can display but not
execute to completion.

Fields:
- `boundaryType`: `share`, `photo-library`, `camera`, `review`, `subscription`,
  `legal`, `watch`, `integration`, or `diagnostic-logs`.
- `route`: boundary placeholder route.
- `originRoute`: route that requested the boundary.
- `canTransmit`: false for this feature.
- `requiredFutureOwner`: spec that may implement the final action later.
- `safeExitRoute`: return target.

Validation:
- `canTransmit` must remain false in this feature.
- Every boundary must have a safe exit route.
- Every final action must have a future owner or remain explicitly blocked.

## Entity: RiskyActionGate

Represents a destructive, account-changing, transmitting, or external final
action.

Fields:
- `actionId`: stable action identifier.
- `label`: user-facing action label.
- `category`: `destructive`, `account`, `transmission`, `external`,
  `integration`, or `privacy`.
- `sourceScreens`: evidence screen IDs.
- `gateType`: `blocked`, `confirm-required`, or `external-leaf`.
- `ownerSpec`: current or future owning spec.

Validation:
- No risky action may have `gateType` omitted.
- `blocked` actions must show a non-executing placeholder.
- `confirm-required` actions must not execute in this feature.

## Entity: PlaceholderSurface

Represents a shell-owned stand-in for a later feature surface.

Fields:
- `surfaceId`: stable placeholder identifier.
- `ownerSpec`: future owning spec.
- `route`: RouteEntry pathname.
- `sourceScreens`: source evidence screen IDs.
- `summary`: what the placeholder represents.
- `availableActions`: actions that route to other placeholders or boundaries.

Validation:
- Placeholder copy must not claim completed business behavior.
- Placeholder must preserve route, header, action, and return contracts.

## Relationships

- AppTab has many RouteEntry defaults.
- RouteEntry may open many OverlayState entries.
- RouteEntry may open many NativeIntentBoundary entries.
- RiskyActionGate belongs to RouteEntry or OverlayState.
- PlaceholderSurface is implemented by RouteEntry and later replaced by its
  ownerSpec implementation.

## State Transitions

- Primary tab navigation: `home` <-> `library` <-> `trends` <-> `profile`.
- Stack route open: AppTab route -> stack RouteEntry -> origin AppTab route.
- Modal route open: RouteEntry -> OverlayState -> RouteEntry.
- Native boundary open: RouteEntry -> NativeIntentBoundary -> RouteEntry.
- Unknown path: any invalid path -> NotFound route -> safe top-level tab.
