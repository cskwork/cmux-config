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
