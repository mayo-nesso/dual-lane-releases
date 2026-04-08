# DualLane

A macOS app switcher with two lanes. Assign your most-used apps to the primary lane and switch between them faster.

## How it works

Press **Cmd+Tab** to open the switcher. Apps are split into two rows:

- **Primary lane** — your go-to apps, configured by you
- **Secondary lane** — everything else

| Key | Action |
|-----|--------|
| `Cmd+Tab` | Open switcher / next app |
| `Cmd+Shift+Tab` | Previous app |
| `← / →` | Navigate within lane |
| `` ` `` or `↑ / ↓` | Switch between lanes |
| `S` | Move selected app to the other lane |
| Scroll wheel | Navigate within lane |
| Release `Cmd` | Activate selected app |
| Click | Activate app immediately |
| `Esc` or click outside | Dismiss without switching |

Switch-lane and move-to-lane keys are configurable via Settings.

The switcher is suppressed when Mission Control or App Exposé is active.

The menu bar icon (▪︎▪︎) lets you assign apps to lanes — persisted across launches.

Apps with multiple instances running show a numbered badge. Each instance can be assigned to a different lane independently.

---

## Setup

### Requirements

- macOS 13.5 or later
- Xcode 16 or later

### Build and run

```bash
cd scripts
bash run.sh
```

This will run all tests, build the app, copy it to `/Applications`, and launch it. The script aborts if any test fails.

### Grant Accessibility permission

On first launch macOS will prompt for Accessibility access — this is required for `Cmd+Tab` interception.

If the prompt doesn't appear:

> **System Settings → Privacy & Security → Accessibility** → enable DualLane

### Space management tip

If switching apps causes macOS to reorder your Spaces, disable:

> **System Settings → Desktop & Dock → Mission Control → Automatically rearrange Spaces based on most recent use**

---

## Settings

Open the Settings window from the menu bar popover header. The **General** tab exposes:

- **Icon size** — configurable min and max (in points); auto-scales with the number of open apps
- **Switcher position** — vertical placement on screen (Top / Middle Top / Middle / Middle Bottom / Bottom)
- **Scroll sensitivity** — how far to scroll before the selection advances (Low / Medium / High)
- **Show on all displays** — show the overlay on every monitor, or only the one with the cursor

The **Keys** tab lets you add or remove switch-lane and move-to-lane key bindings using the built-in key recorder.

---

## Customization

For changes not covered by Settings:

- **Hotkey intercept keys** (Cmd+Tab itself): edit `HotKeyMonitor.swift` — the `kVK_*` constants
- **HUD style**: edit `UI/Switcher/SwitcherOverlayView.swift`
