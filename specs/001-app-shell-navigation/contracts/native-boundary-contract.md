# Contract: Native and External Boundaries

## Purpose

Define how the shell represents native/external handoffs without performing
final actions in Feature 001.

## Boundary Types

| Boundary Type | Source Evidence | Future Owner | Feature 001 Behavior |
| --- | --- | --- | --- |
| `share` | S022, S045, S107, S123, S227, S232 | 017 | Show non-transmitting placeholder and allow back/cancel |
| `photo-library` | S076 | 006 | Show media boundary placeholder and allow back/cancel |
| `camera` | S079 | 006 | Show camera boundary placeholder and allow back/cancel |
| `review` | S114 | 015/017 | Show review boundary placeholder and allow Not Now/back |
| `subscription` | S119 | 015/017 | Show external subscription placeholder and allow back |
| `legal` | S129, S131 | 015/017 | Show legal WebView placeholder and allow back |
| `watch` | S019, S032, S104 | 017 | Show watch-send placeholder/result and return to origin |
| `integration` | S121 | 015/017 | Show provider placeholder and return to devices |
| `diagnostic-logs` | S118 | 015/017 | Show blocked/confirm-required placeholder |

## Required Behavior

- The shell must never select a native share target.
- The shell must never take or upload a photo.
- The shell must never send messages or diagnostic logs.
- The shell must never connect or disconnect integrations.
- The shell must never open billing/account destructive actions as final flows.
- Every boundary must have a visible safe-exit path.

## Incoming Native Intents

`app/+native-intent.tsx` must defensively rewrite unsupported or malformed
incoming paths to a safe route. It must not throw. Unexpected paths should route
to a recoverable not-found or error placeholder.

## Future Ownership Rule

A later feature may replace a boundary placeholder only when its spec defines:
- final action confirmation rules
- success state
- cancel state
- error state
- privacy/transmission behavior
- return behavior
