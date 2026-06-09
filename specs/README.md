# Spec Coverage Index

This directory decomposes APP_ARCHITECTURE.md into Spec Kit feature boundaries.
Each feature spec is intentionally technology-agnostic and evidence-backed by
manual-navigation-map/NAVIGATION.md, screenshots, and state dumps.

| Spec | Work Package | Scope |
| --- | --- | --- |
| 001-app-shell-navigation | 1 | App shell, primary tabs, stack routing, modal/sheet host, native boundary placeholders |
| 002-workout-detail-data-model | 2 | Workout domain model and shared Workout Detail UI contract |
| 003-generate-workout-flow | 3 | Generate Workout wizard and generated result flow |
| 004-custom-workout-editor | 4 | Custom workout editor, sections, set groups, set controls |
| 005-saved-workout-library | 5 | Saved workouts, save-to-library, delete-safe library flows |
| 006-image-import-workout | 6 | Image import choices, camera/photo native boundaries, OCR handoff contract |
| 007-start-workout-splash-mode | 7 | Start menu and Splash Mode guided player |
| 008-manual-log-post-log | 8 | Manual log, post-log home/profile/trends updates |
| 009-completed-workout-share-export | 9 | Completed workout detail, edit, social share preview, PDF export |
| 010-library-browse-catalogs | 10 | Library tab, WOD history, categories, filters, plan catalog entry |
| 011-training-plans | 11 | Plan generation, catalog/detail, active plan and plan workout linkage |
| 012-home-dashboards | 12 | Home empty, active-plan, and post-log dashboards |
| 013-trends-analytics | 13 | Monthly analytics dashboard and metric cards |
| 014-profile-achievements-history | 14 | Profile tabs, achievements, history, swim profile preferences |
| 015-settings-account-integrations | 15 | Settings, account, devices, privacy, legal, review/share/log leaves |
| 016-support-coach-chat | 16 | Support/help center and Coach Chat surfaces |
| 017-external-integrations-export | 17 | Watch send, native share, PDF, review, legal WebView integration boundaries |
| 018-qa-matrix | 18 | Cross-feature QA matrix for risky actions, returns, states, shared flow duplicates |

Planning order should follow APP_ARCHITECTURE.md MVP Sequencing unless a later
feature spec records a smaller independently testable boundary.
