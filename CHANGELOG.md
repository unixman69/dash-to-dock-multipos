# Changelog

All notable changes in this fork relative to its base, the upstream
[Dash to Dock](https://github.com/micheleg/dash-to-dock) **v105** release.

This fork adds per-monitor dock positioning on top of upstream and carries a
few GNOME 50 compatibility and bug fixes. Versions below are the extension
`metadata.json` version numbers.

The three general-purpose changes (per-monitor positions, the freshly-started
minimize fix, and the Settings-item focus fix) have been submitted upstream as
pull requests — see the note at the end.

## [109] — 2026-07-21

### Fixed
- Dock no longer flickers in and out when an application repeatedly reads the
  clipboard (for example a terminal running a clipboard-watching tool).
  wl-clipboard maps a short-lived invisible helper window on every clipboard
  access, which briefly became the top window and confused intellihide; such
  helper windows are now ignored.

## [108] — 2026-07-19

### Fixed
- GNOME 50 compatibility: guard against the removal of
  `Clutter.Event.get_click_count()`. On GNOME 50 reading it threw and aborted
  the icon click handler, so click actions (including minimize) silently did
  nothing. Older shells keep full double-click detection.
- Double-click detection now reads the click count from button-release events,
  matching how icon activation is actually delivered.

### Changed
- Per-monitor position labels are now translatable and rebuild when the
  overrides change from outside the preferences dialog.

### Packaging
- The extension now ships its own copy of the upstream settings schema and
  compiles it into the extension directory, so it is self-contained and no
  longer depends on the original Dash to Dock being installed for its schema.
  (Fork-only; not applicable upstream.)

## [107] — 2026-07-16

Maintenance release — version bump only, no functional changes.

## [106] — 2026-07-12

### Added
- **Per-monitor dock position.** Each connected monitor can have its own dock
  edge (top/right/bottom/left), configured per monitor on the Position and Size
  settings page. Monitors without an override follow the global dock position.
  Overrides are stored in a separate fork-only settings schema.

### Fixed
- Minimize click action no longer fails on freshly started applications, where
  a stale cached focus/running state could be computed while the app was still
  starting. State is now recomputed at click time.
- The Settings menu item focuses an already-open preferences window instead of
  silently doing nothing when the dialog is already up.

### Changed
- Renamed the global "Position on screen" preference to "Global position on
  screen" to distinguish it from the new per-monitor overrides.
- Synced with upstream `master` (post-v105 fixes, snapshot `248d42b`).

## [105] — base

Upstream Dash to Dock v105 (`micheleg/dash-to-dock`, tag for GNOME 45–48),
imported unchanged as the starting point for this fork.

---

## Upstream pull requests

The general-purpose changes have been offered back to upstream Dash to Dock as
pull requests from `unixman69/dash-to-dock` (all currently open):

- [#2645](https://github.com/micheleg/dash-to-dock/pull/2645) — Add per-monitor dock position overrides
- [#2647](https://github.com/micheleg/dash-to-dock/pull/2647) — Fix stale cached focus state breaking click actions
- [#2648](https://github.com/micheleg/dash-to-dock/pull/2648) — Focus the already-open prefs window from the Settings item

The GNOME 50 `get_click_count` guard and the wl-clipboard intellihide fix are
not yet upstream.
