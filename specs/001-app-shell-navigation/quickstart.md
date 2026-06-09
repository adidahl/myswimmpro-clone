# Quickstart: App Shell and Navigation Foundation

## Prerequisites

- Node.js available locally.
- Expo CLI available through `npx`.
- Dependencies installed after implementation.

## Setup

If the Expo app has not been scaffolded yet, implementation tasks will create a
temporary SDK 55 template and merge the app scaffold into the existing repo:

```bash
npx create-expo-app@latest .tmp/expo-template --template default@sdk-55
```

After implementation tasks have merged the scaffold and created `package.json`,
run from repository root:

```bash
npm install
```

## Validation Commands

```bash
npm run typecheck
npm run lint
npm test
npx expo start --web
```

Expected outcomes:
- Typecheck completes with no errors.
- Lint completes with no blocking issues.
- Route tests pass for primary tabs, shared routes, and native boundaries.
- Expo web opens to Home with Home tab active.

## Manual Smoke Scenario 1: Primary Tabs

1. Start the app.
2. Confirm Home opens first.
3. Select Library, Trends, Profile, then Home.
4. Confirm the active tab and placeholder content match the tab role.

Evidence references: S001, S115, S116, S117, S176, S180, S181.

## Manual Smoke Scenario 2: Shared Routes and Overlays

1. From Home, open a representative Workout Detail placeholder.
2. Open Start Menu placeholder.
3. Close Start Menu.
4. Back out to Home.
5. Open Support and close it.

Evidence references: S007, S008, S010, S033, S149, S150.

## Manual Smoke Scenario 3: Native Boundaries

1. Open a share boundary placeholder.
2. Back out without selecting a target.
3. Open photo-library and camera placeholders.
4. Back out from each.
5. Confirm no upload, message send, account mutation, or transmission occurs.

Evidence references: S022, S075, S076, S079, S123, S227.

## Manual Smoke Scenario 4: Post-Log Tab Returns

1. Enable the post-log fixture state.
2. Visit Library, Trends, Profile, and Home.
3. Confirm tab returns align with S247-S250 evidence.

Evidence references: S247, S248, S249, S250.

## Acceptance Gate

Do not start implementation of feature-specific packages until:
- `tasks.md` is complete.
- `analysis.md` reports no critical issues.
- The shell route registry has explicit owner specs for placeholders.
