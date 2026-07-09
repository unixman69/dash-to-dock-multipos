# Dash to Dock (Multi-Position)

A fork of [Dash to Dock](https://github.com/micheleg/dash-to-dock) that adds
**per-monitor dock position**: each monitor can place its dock on a different
edge (top, right, bottom or left), instead of every dock sharing one global
position.

All credit for Dash to Dock itself goes to
[Michele Gaio and contributors](https://github.com/micheleg/dash-to-dock).
This fork is based on the upstream **v105** release and, like upstream, is
licensed under the [GPL-2.0](COPYING).

## What it adds

- In **Settings → Position and size**, below *Show the dock on*, there is one
  row per connected monitor with a dropdown:
  **Follow global setting / Top / Right / Bottom / Left**.
- Monitors set to *Follow global setting* behave exactly like stock Dash to
  Dock. Choosing a side overrides the position for that monitor only, and
  applies immediately.
- Overrides are keyed by the monitor's connector name (e.g. `DP-4`), so they
  survive unplugging and replugging and never leak onto other monitors.
- Everything else — settings, themes, behavior — is unchanged from stock, and
  the stock settings are shared: if you switch between this fork and the
  original extension, all your preferences carry over. The per-monitor
  overrides live in a separate, fork-only GSettings schema.

## Installation

```bash
git clone https://github.com/unixman69/dash-to-dock-multipos.git \
    ~/.local/share/gnome-shell/extensions/dash-to-dock-multipos@unixman69
glib-compile-schemas \
    ~/.local/share/gnome-shell/extensions/dash-to-dock-multipos@unixman69/schemas/
```

Log out and back in (required on Wayland), then:

```bash
gnome-extensions enable dash-to-dock-multipos@unixman69
```

**Important:** this fork and the original Dash to Dock are separate
extensions that would fight over the same dock. Enable one or the other,
never both.

## Compatibility

GNOME Shell 45–50 (same as upstream v105). Developed and tested on
GNOME 50.3.

## Relation to upstream

This fork exists because upstream's `dock-position` is a single global
setting. The change set is small and self-contained (an optional
`monitorIndex` argument threaded through `Utils.getPosition()` plus a
connector-keyed override map) and is offered upstream — if it lands there,
this fork becomes obsolete, which is the best possible outcome.
