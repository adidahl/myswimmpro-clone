# Feature Specification: Trends Analytics Dashboard

**Feature Branch**: `013-trends-analytics`
**Created**: 2026-06-09
**Status**: Draft
**Input**: Work package 13 from APP_ARCHITECTURE.md.

## Architecture Evidence

- **Architecture source**: APP_ARCHITECTURE.md Trends Routes, Trends module, Activity + Trends Domain.
- **Source screen clusters**: S116, S176-S179, S248.
- **Referenced screens**: S116, S176, S177, S178, S248.
- **Explicitly out of scope**: Manual log creation, profile history, deep analytics beyond visible monthly cards.

## User Scenarios & Testing

### User Story 1 - View Monthly Stats (Priority: P1)

As a swimmer, I can open Trends and see monthly stat cards for distance, duration, average workout metrics, pace, and SWOLF.

**Independent Test**: Open Trends with empty and logged fixtures and confirm cards render expected values.

### User Story 2 - Refresh After Logging (Priority: P2)

As a swimmer, after logging a workout, I can return to Trends and see updated metrics.

**Independent Test**: Apply post-log fixture and verify Trends changes from empty/zero to logged values.

### User Story 3 - Reach Support From Trends (Priority: P3)

As a swimmer, I can open Support from Trends and return to Trends.

**Independent Test**: Open Support from Trends and close it.

## Requirements

- **FR-001**: Trends MUST show monthly cards for total distance, total duration, average workout distance/duration, pace, SWOLF, and future metric placeholders.
- **FR-002**: Trends MUST support empty/zero and logged states.
- **FR-003**: Trends MUST refresh when ActivityLog changes.
- **SR-001**: Loading, empty, partial metric, calculation error, offline, and support return states MUST be defined.
- **SR-002**: Metrics MUST be traceable to ActivityLog and ActivityMetric definitions.

## Key Entities

- **TrendMetricCard**: Metric label, value, unit, period, and state.
- **MonthlyTrendSummary**: Aggregated monthly activity metrics.
- **TrendRefreshTrigger**: Activity changes that invalidate trends.

## Success Criteria

- **SC-001**: Empty and logged Trends states are independently demonstrable.
- **SC-002**: Post-log fixture updates at least total distance and total duration.
- **SC-003**: Support return from Trends preserves active Trends tab.

## Assumptions

- Advanced analytics can be added after visible card contracts are stable.
- Initial metric calculations may use deterministic fixtures.
