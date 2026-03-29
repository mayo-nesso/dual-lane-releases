# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2026-03-29

### Fixed

- Switcher popup now stays horizontally centered as more apps are added. The window width formula was not accounting for `AppIconCell`'s cell padding (+12 pt) or the full side padding of the overlay (72 pt), causing `NSHostingView` to auto-resize the window from its left edge and push it off-center.
- Switcher popup now resizes and recenters immediately when an app is moved between lanes (primary ↔ secondary), instead of requiring the switcher to be closed and reopened.

## [1.0.0] - 2026-03-01

### Added

- Initial release.
