<p align="center">
  <img src="../../koci-logo.svg" alt="Koci logo" width="120" />
</p>

<h1 align="center">koci-atcommands</h1>

<p align="center">
  Player <code>@commands</code> for everyone, each switchable in Settings.
</p>

## What it does

Normal players have no `@commands` by default. This mod gives **every player** (group `Id: 0`) the `@commands` you choose, so friends and family can spawn items, raise stats, get Zeny and so on without a GM account.

Every command is its own on/off setting under **Settings → Mods → koci-atcommands**. All are ticked by default once the mod itself is enabled, so untick the ones you don't want. The mod is **off by default**.

## How it works

Each command is a boolean setting whose key is the rAthena command name. For each one there is a file `conf/when/<command>/groups.yml` that lists the command under `Commands:` for group 0. The app merges that file in only while the setting is on. Applying settings restarts the server.

## Commands

### Character

| Command | What it does |
| --- | --- |
| `@baselevelup` | Raises your base level the desired number of levels. |
| `@joblevelup` | Raises your job level the desired number of levels. |
| `@jobchange` | Changes your job. |
| `@allskill` | Gives you all skills. |
| `@charcommands` | Displays a list of charcommands that you can use. |

### Stats

| Command | What it does |
| --- | --- |
| `@str` | Raises STR by given amount. |
| `@agi` | Raises AGI by given amount. |
| `@vit` | Raises VIT by given amount. |
| `@int` | Raises INT by given amount. |
| `@dex` | Raises DEX by given amount. |
| `@luk` | Raises LUK by given amount. |
| `@pow` | Raises POW by given amount. |
| `@sta` | Raises STA by given amount. |
| `@spl` | Raises SPL by given amount. |
| `@con` | Raises CON by given amount. |
| `@crt` | Raises CRT by given amount. |

### Items

| Command | What it does |
| --- | --- |
| `@item` | Gives you the desired item. |
| `@refine` | Refines the equipment in a given position by a +/- amount. |
| `@grade` | Changes the grade of the equipment in a given position by a +/- amount. |
| `@costume` | Changes the player's visible appearance to the selected costume. |

### Economy

| Command | What it does |
| --- | --- |
| `@zeny` | Gives you the desired amount of Zeny. |
| `@cash` | Gives you the specified amount of cash points. |
| `@points` | Gives you the specified amount of Kafra Points. |

### Loot

| Command | What it does |
| --- | --- |
| `@autoloot` | Makes items go straight into your inventory. |
| `@autolootitem` | Makes items of specific item IDs go straight into your inventory. |

### Monsters

| Command | What it does |
| --- | --- |
| `@monster` | Spawns the desired monster. |
| `@mobsearch` | Shows the location of a certain monster on the current map. |
| `@whereis` | Displays the maps in which a monster normally spawns. |
| `@whodrops` | Shows who drops an item (monster with highest drop rates). |

### Pets & Homunculus

| Command | What it does |
| --- | --- |
| `@hatch` | Creates a pet from your inventory eggs list. |
| `@homevolution` | Evolves your homunculus, if possible. |
| `@homfriendly` | Sets your homunculus intimacy level to the desired value (0-1000). |
| `@hominfo` | Displays homunculus stats. |
| `@homlevel` | Increases the homunculus level by the given amount. |

### Mounts

| Command | What it does |
| --- | --- |
| `@cart` | Gives or removes a cart and changes the cart skin. |
| `@mount_peco` | Gives or removes a job-based mount. |

### Guild

| Command | What it does |
| --- | --- |
| `@guild` | Creates a guild. |
| `@guildlevelup` | Raises your guild by the desired number of levels. |

## Requirements

Ragnarok Offline `>=1.2.6`, any era.
