# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.4.0] - 2026-05-01

### Fixed

- Mouse wheel scroll now correctly navigates between icons in the switcher. The integer line-delta field (`scrollWheelEventDeltaAxis1`) was returning 0 for many physical mice when captured via `CGEventTap`; switched to the fixed-point field (`scrollWheelEventFixedPtDeltaAxis1`) which is reliably populated.

## [1.3.0] - 2026-04-24

### Added

- New "Always show app names" toggle in Settings → Display. When off (default), only the selected app's name is shown, matching native macOS switcher behaviour. When on, all names are visible at once.

### Fixed

- Switcher opening slowly (~3 s) when Unity Editor (or other apps with multiple instances sharing a bundle ID) was running — window title lookups via Accessibility API now happen lazily on a background thread only for the currently selected app, instead of blocking the main thread for every app on each open.
- App names are now hidden for non-selected cells (matching native macOS switcher behaviour); the window title of a duplicate-instance app is shown only when that app is selected.

## [1.2.0] - 2026-04-14

### Added

- Hide/show individual apps from Lane Config — new **H** button in each app row; hidden apps are removed from the switcher overlay and their state persists to disk.
- Assigning a hidden app to a lane (Primary or Secondary) automatically unhides it.

### Fixed

- Settings window disappearing when the app lost and regained focus; the app is now activated before the window is shown.

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

### Added

- Settings window (General and Keys tabs) accessible from the menu bar popover.
- About tab in Settings showing the app icon, version number, and a Ko-fi support link.
- Version number displayed in the switcher overlay (bottom-right corner) and the menu bar popover header.
- App icon.
- Multi-display support: overlay can appear on the active display or all displays simultaneously.
- Scroll-wheel navigation in the switcher overlay with configurable sensitivity.
- Cancel the switcher via **Escape** or a click outside the overlay — dismisses without activating any app.
- Suppression of the switcher during Mission Control and App Exposé; Cmd+Tab is swallowed while App Exposé is active.
- Space-aware anchoring: the switcher re-attaches to the current Space after a Space transition.
- Configurable switch-lane and move-to-lane hotkeys via a dynamic +/− list with an inline key recorder.
- Overlay hint text updates dynamically to reflect the currently configured hotkeys.
- **§** key added as an additional switch-lane binding for ISO keyboards.
- Move the selected app to the other lane directly from the switcher overlay.
- Per-PID lane overrides for apps with multiple running instances; duplicate instances shown with a numeric badge and desaturation.
- Accessibility permission warning banner in the Lane Config header (tapping opens System Settings).
- Accessibility permission status row in General settings.
- Configurable switcher vertical position in General settings.
- Configurable icon size range (min/max) with a Reset button in General settings.
- Unit tests for `LaneManager`, `SwitcherViewModel`, and activation order.

### Fixed

- Switcher popup now stays horizontally centered as more apps are added. The window width formula was not accounting for `AppIconCell`'s cell padding (+12 pt) or the full side padding of the overlay (72 pt), causing `NSHostingView` to auto-resize the window from its left edge and push it off-center.
- Switcher popup now resizes and recenters immediately when an app is moved between lanes (primary ↔ secondary), instead of requiring the switcher to be closed and reopened.

## [1.0.0] - 2026-03-01

### Added

- Initial release: macOS dual-lane app switcher intercepting Cmd+Tab globally.
- Two-lane overlay (Primary and Secondary) with app icons; navigate forward/backward with Cmd+Tab / Cmd+Shift+Tab and switch lanes with arrow keys.
- Release Cmd to activate the selected app; Esc to dismiss without switching.
- Menu bar icon with a Lane Config popover for assigning apps to lanes; assignments persist across launches.
[Unreleased]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.4.0...HEAD
[1.4.0]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.3.1-alpha.1...v1.4.0
[1.3.1-alpha.1]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.3.0...v1.3.1-alpha.1
[1.3.0]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.2.1-alpha.5...v1.3.0
[1.2.1-alpha.5]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.2.1-alpha.4...v1.2.1-alpha.5
[1.2.1-alpha.4]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.2.1-alpha.3...v1.2.1-alpha.4
[1.2.1-alpha.3]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.2.1-alpha.2...v1.2.1-alpha.3
[1.2.1-alpha.2]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.2.1-alpha.1...v1.2.1-alpha.2
[1.2.1-alpha.1]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.2.0...v1.2.1-alpha.1
[1.2.0]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.1.1...v1.2.0
[1.1.1]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.1.0...v1.1.1
[1.1.0]: https://github.com/mayo-nesso/dual-lane-macos/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/mayo-nesso/dual-lane-macos/releases/tag/v1.0.0
