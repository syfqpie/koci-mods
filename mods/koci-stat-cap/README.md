<p align="center">
  <img src="../../koci-logo.svg" alt="Koci logo" width="120" />
</p>

<h1 align="center">koci-stat-cap</h1>

<p align="center">
  Raise the maximum STR/AGI/VIT/INT/DEX/LUK for every job.
</p>

## What it does

Each job category has a stat cap (for example 99 for a novice line, 130 for third jobs). This mod raises the cap for **all job categories** to one value you choose: normal, baby, transcendent, third, transcendent third, baby third, extended, summoner and fourth jobs. Default is 500.

It only raises the *cap*. You still need stat points to spend (or the `@str`-style commands from `koci-atcommands`) to actually reach it.

## Settings

| Setting | Default | Description |
| --- | --- | --- |
| Maximum stat value (`max_stat`) | 500 (1 to 1000) | Highest value STR, AGI, VIT, INT, DEX and LUK can reach. |

## How it works

`npc/stat_cap.txt` runs once when the server starts. It sets rAthena's nine `max_*_parameter` battle flags to the chosen value, then runs `@reloadpcdb`. The reload is needed because the server copies those flags into each job's max stats while the player database loads, before any script runs. Setting the flags alone has no effect.

## Notes

- Changing the setting needs **Apply**, which restarts the server.
- Another mod that sets explicit `MaxStats` in a job table will override this one for that job.

## Requirements

Ragnarok Offline `>=1.2.6`, any era.
