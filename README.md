# cmux-config

Personal configuration for [cmux](https://github.com/manaflow-ai/cmux) — the macOS terminal/workspace app from manaflow-ai.

This repo tracks the file-managed portion of cmux settings (`~/.config/cmux/cmux.json`) so the setup is portable across machines.

Landing page: https://cskwork.github.io/cmux-config/

## What's in here

- **`cmux.json`** — JSONC config consumed by cmux at launch. The full schema template is preserved as commented blocks; only intentionally overridden keys are active.

### Active overrides

| Key | Value | Plist source |
|---|---|---|
| `app.appearance` | `"dark"` | `appearanceMode` |

Everything else falls back to either the in-app Settings value or the schema default. Window geometry, file-explorer width, Sparkle update state, and other transient runtime state are intentionally not file-managed.

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
