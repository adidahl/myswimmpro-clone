# Contract: Route Registry and Ownership

## Purpose

Define the shell route contract that later feature specs can consume without
changing primary navigation behavior.

## Primary Tabs

| Route | Tab | Owner | Source Evidence | Required State |
| --- | --- | --- | --- | --- |
| `/` | Home | 001 | S001, S142, S179, S250 | Active Home tab |
| `/library` | Library | 001 | S115, S151, S181, S247 | Active Library tab |
| `/trends` | Trends | 001 | S116, S176, S248 | Active Trends tab |
| `/profile` | Profile | 001 | S117, S180, S249 | Active Profile tab |

## Shell-Owned Placeholder Routes

| Route Pattern | Presentation | Placeholder Owner | Future Owner | Return Behavior |
| --- | --- | --- | --- | --- |
| `/workout/[workoutId]` | stack | 001 | 002 | Back to origin tab or origin route |
| `/modal/start-menu` | modal | 001 | 007 | Close/back to workout detail |
| `/modal/import-workout` | modal | 001 | 006 | Close/back to origin tab |
| `/support` | stack | 001 | 016 | Close/back to origin tab |
| `/support/messages` | stack | 001 | 016 | Back to Support |
| `/coach-chat/[scopeType]/[scopeId]` | stack | 001 | 016 | Back to origin route |
| `/native-boundary/[boundaryType]` | native-boundary | 001 | 017 | Back to origin route |
| `/*` | not-found | 001 | 001 | Safe top-level fallback |

## Route Metadata Requirements

Every route entry must include:
- stable ID
- pathname or route pattern
- presentation type
- owner spec
- source evidence screen IDs
- return behavior
- allowed actions
- risky action gates, if any

## Return Behavior Rules

- Tab to tab: active tab changes and no stack placeholder is opened.
- Stack from tab: back returns to originating tab.
- Stack from stack: back returns to previous stack route.
- Modal from stack: close/back returns to underlying route with no mutation.
- Native boundary from any route: back/cancel returns to origin route and no
  transmission occurs.
- Not found: show safe state and provide Home return.

## Non-Goals

- This contract does not define workout data rendering beyond placeholder copy.
- This contract does not perform external native actions.
- This contract does not own feature-specific API contracts.
