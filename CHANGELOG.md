# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.2.0] - 2026-04-14

## [1.1.1] - 2026-04-07

### Added

- Event tap now runs on a dedicated high-priority thread, keeping it responsive under CPU load.
- Watchdog timer restarts the event tap if it stops firing (aggressive tap recovery).
- Cross-thread state protected with `os_unfair_lock` to prevent race conditions.
- `runningApplications` cache and warm window pool pre-allocated at startup to reduce first-open latency.
- App Exposé window tracking now uses an event-driven `AXObserver` instead of polling.

### Changed

- Lane assignments now persist to Application Support instead of UserDefaults.

### Fixed

- Event thread run loop kept alive with a dummy source so it does not exit between events.
- Momentum scroll events swallowed in the switcher to prevent phantom navigation after a trackpad flick.

## [1.1.0] - 2026-03-29

### Fixed

- Switcher popup now stays horizontally centered as more apps are added. The window width formula was not accounting for `AppIconCell`'s cell padding (+12 pt) or the full side padding of the overlay (72 pt), causing `NSHostingView` to auto-resize the window from its left edge and push it off-center.
- Switcher popup now resizes and recenters immediately when an app is moved between lanes (primary ↔ secondary), instead of requiring the switcher to be closed and reopened.

## [1.0.0] - 2026-03-01

### Added

- Initial release.
[Unreleased]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.2.0...HEAD
[1.2.0]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.1.1...v1.2.0
[1.1.1]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.1.0...v1.1.1
[1.1.0]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/mayo-nesso/dual-lane-macos/releases/tag/v1.0.0
