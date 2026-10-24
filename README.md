<p align="center">
  <img src="./koci-logo.svg" alt="Koci logo" width="160" />
</p>

<h1 align="center">koci-mods</h1>

<p align="center">
  A collection of mods for <a href="https://github.com/Flux159/ragnarokoffline.app">Ragnarok Offline</a>, made for fun.
</p>

## About

These are the mods I use in my own Ragnarok Offline setup, for casual play with friends and family. They favour convenience and fun over balance, so they aren't meant for competitive or online servers.

## Mods

All mods are disabled by default. Enable the ones you want in the app.

| Mod                               | Purpose                                                                                                                                  |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| [`atcommands`](./mods/atcommands) | Player `@commands` for everyone (38 of them), each switchable in Settings: character, stats, items, economy, loot, monsters, pets, mounts and guild. |
| [`stat-cap`](./mods/stat-cap)     | Sets the maximum STR/AGI/VIT/INT/DEX/LUK for every job category, including transcendent, baby, third, fourth and summoner classes.       |

## Installing

1. Download the mod's ZIP (e.g. `atcommands.zip`) from the [Releases](../../releases) page.
2. Import it in Ragnarok Offline's mod manager.
3. Turn the mod on and adjust its settings.

Each ZIP contains the mod folder at its root. Requires Ragnarok Offline `>=1.2.6`.

## Project structure

```
.
├── mods/
│   ├── atcommands/
│   │   ├── mod.json                  # manifest: name, version, requires, settings
│   │   └── conf/
│   │       └── when/<command>/       # groups.yml merged in only while that setting is on
│   └── stat-cap/
│       ├── mod.json
│       └── npc/                      # NPC script that applies the stat cap
├── .github/workflows/release.yml     # zips each mod on release
└── koci-logo.svg
```

There is no build system, package manager or test suite. Each mod is a directory of configuration files that mirrors the game's data layout.

## Adding to a mod

- **New at-command**: add a boolean setting to `mods/atcommands/mod.json` with the rAthena command name as `key` and a `Category:` prefix in `label`, then add `conf/when/<key>/groups.yml`. Check names against rAthena's `conf/atcommands.yml`.
- **New mod**: create `mods/<name>/mod.json`, keep `"default": "off"`, and set `requires`. See the [modding reference](https://github.com/Flux159/ragnarokoffline.app/blob/main/docs/MODDING.md) (max 40 settings per mod).

Bump `version` in the mod's `mod.json` with every change.

## Releasing

Publishing a GitHub Release triggers `.github/workflows/release.yml`, which zips each `mods/*/` directory to `dist/<mod_name>.zip` and attaches the files to the release. New directories under `mods/` are picked up automatically.
