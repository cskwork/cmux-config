# cmux-config

Personal configuration for [cmux](https://github.com/manaflow-ai/cmux) — the macOS terminal/workspace app from manaflow-ai.

This repo tracks the file-managed portion of cmux settings (`~/.config/cmux/cmux.json`) so the setup is portable across machines.

Landing page: https://cskwork.github.io/cmux-config/

## What's in here

- **`cmux.json`** — JSONC config consumed by cmux at launch. The full schema template is preserved as commented blocks; only intentionally overridden keys are active.

### Active overrides

| Key | Value | Schema default | Plist source |
|---|---|---|---|
| `app.appearance` | `"dark"` | `"system"` | `appearanceMode` |
| `app.sendAnonymousTelemetry` | `false` | `true` | (not persisted in plist; file-managed to enforce opt-out across machines) |
| `sidebarAppearance.tintOpacity` | `0.18` | `0.03` | `sidebarTintOpacity` |

Everything else falls back to either the in-app Settings value or the schema default. Window geometry, file-explorer width, Sparkle update state, and other transient runtime state are intentionally not file-managed.

### Settings the cmux.json schema can't manage yet

The following keys exist in the macOS plist but are not exposed in cmux's published JSON schema, so they cannot be put in `cmux.json` today:

- `sidebarMaterial`, `sidebarBlendMode`, `sidebarPreset`, `sidebarState`, `sidebarBlurOpacity`, `sidebarCornerRadius`

If you want these portable, set them once via the in-app Settings panel on a new machine.

## Ghostty config (cmux's embedded terminal)

cmux embeds [Ghostty](https://ghostty.org) as its terminal renderer (you can see this in the cmux binary symbols: `Ghostty version`, `GhosttyBackgroundBlur`, `ghostty.backgroundColor`, etc.). Anything you customize on the terminal pane itself — font, background image, opacity, custom shaders — is a **Ghostty** setting, not a cmux setting, and lives in `~/.config/ghostty/config`.

This repo therefore also tracks a small Ghostty config that goes hand-in-hand with the cmux setup:

```
ghostty/
├── config.ghostty                  # font + background-image overrides
└── backdrops/
    └── cloudy-quasar.png           # 3840x2160 PNG referenced by config
```

### Active Ghostty overrides

| Key | Value | Ghostty default |
|---|---|---|
| `font-family` | `JetBrainsMono Nerd Font` | system mono |
| `font-style` | `Medium` | `Regular` |
| `font-size` | `15` | `13` |
| `background-image` | `~/.config/ghostty/backdrops/cloudy-quasar.png` | (none) |
| `background-image-fit` | `cover` | `tile` |
| `background-image-position` | `center` | `tl` |
| `background-image-opacity` | `0.18` | `1.0` |

### Apply on a new machine

```sh
mkdir -p ~/.config/ghostty/backdrops
cp ghostty/config.ghostty ~/.config/ghostty/config
cp ghostty/backdrops/cloudy-quasar.png ~/.config/ghostty/backdrops/
```

Note the destination filename is `config` (no extension) — that is Ghostty's canonical config path. The repo keeps the `.ghostty` extension purely as a hint to editors and to avoid colliding with a plain `config` file at the repo root.

Restart cmux (or any other Ghostty surface) to pick up the change. tmux is unrelated here — tmux is a pure-text multiplexer and has no concept of a background image; what you see on the cmux pane comes from Ghostty.

## Apply on a new machine

```sh
mkdir -p ~/.config/cmux
cp cmux.json ~/.config/cmux/cmux.json
```

Then restart cmux, or use `cmd+shift+,` (Reload Configuration) to pick it up without a relaunch.

## Schema reference

cmux validates `cmux.json` against:

```
https://raw.githubusercontent.com/manaflow-ai/cmux/main/web/data/cmux.schema.json
```

Editors that honour the `$schema` field will autocomplete keys and enum values.

## Tested with

- cmux `0.64.9 (89)` on macOS (Darwin 25.4.0)
