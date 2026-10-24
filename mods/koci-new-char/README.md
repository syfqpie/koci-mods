<p align="center">
  <img src="../../koci-logo.svg" alt="Koci logo" width="120" />
</p>

<h1 align="center">koci-new-char</h1>

<p align="center">
  Choose what a new character starts with.
</p>

## What it does

On a character's **first login**, this mod can warp them to a map of your choice, give them Zeny and hand them a set of starter items. It is configurable under **Settings → Mods → koci-new-char**. The mod is **off by default**, and every setting defaults to "do nothing".

## Settings

| Setting | Default | Description |
| --- | --- | --- |
| Spawn map (`start_map`) | empty | Map name to warp to, for example `prontera`. Empty keeps the default spawn. An unknown map is skipped. |
| Spawn X / Y (`start_x`, `start_y`) | 0 | Coordinates on that map. If either is 0, a random spot is used. |
| Starting Zeny (`start_zeny`) | 0 | Zeny given on first login (up to 1,000,000,000). |
| Starter items (`start_items`) | empty | `id:amount` pairs separated by commas, for example `501:50,601:10`. |
| Only characters at base level 1 (`only_new_chars`) | on | Skip characters above base level 1, so existing characters don't get the pack when the mod is first enabled. |

## How it works

`npc/new_char.txt` runs on `OnPCLoginEvent`. It sets a permanent character variable (`newchar_done`) first, so the reward is only ever given once, then adds the Zeny, gives the items and warps the character. Values are read through `F_ModSetting`.

## Notes

- With `only_new_chars` off, every existing character receives the pack once, on their next login.
- A bad item ID is reported in the server log and skipped.
- Changing settings needs **Apply**, which restarts the server.

## Requirements

Ragnarok Offline `>=1.2.6`, any era.
