# Contract: Shell State

## Purpose

Define state names and expectations for the app shell before feature-specific
data exists.

## App Shell State

```ts
type AppShellState =
  | { kind: 'ready'; activeTab: AppTabId; route: string }
  | { kind: 'loading'; activeTab?: AppTabId; route?: string }
  | { kind: 'empty'; activeTab: AppTabId; route: string; reason: string }
  | { kind: 'error'; activeTab?: AppTabId; route?: string; message: string }
  | { kind: 'permissionDenied'; boundaryType: NativeBoundaryType; message: string }
  | { kind: 'offline'; activeTab?: AppTabId; route?: string }
  | { kind: 'notFound'; attemptedPath: string };
```

## Tab State

```ts
type AppTabId = 'home' | 'library' | 'trends' | 'profile';
```

Rules:
- Exactly one primary tab is active while a tab route is focused.
- Stack, modal, and native-boundary routes must preserve origin tab metadata.
- Post-log fixtures must preserve the S247-S250 bottom-tab return contract.

## Placeholder State

```ts
type PlaceholderSurfaceState = {
  surfaceId: string;
  ownerSpec: string;
  sourceScreens: string[];
  title: string;
  summary: string;
  availableActions: string[];
};
```

Rules:
- Placeholder text must identify that the route contract exists without claiming
  feature business logic is complete.
- Available actions must be either shell-owned or delegated to future owner
  specs.

## Overlay State

```ts
type OverlayState = {
  id: string;
  originRoute: string;
  presentation: 'modal' | 'sheet';
  dismissible: true;
  mutatesOnDismiss: false;
};
```

Rules:
- Dismissing an overlay must not mutate business data.
- Overlay hosts must be route-testable.

## Risk State

```ts
type RiskyActionState = {
  actionId: string;
  gateType: 'blocked' | 'confirm-required' | 'external-leaf';
  canExecuteInFeature001: false;
};
```

Rules:
- No RiskyActionState can execute in Feature 001.
- Future specs must change ownership explicitly before execution is allowed.
