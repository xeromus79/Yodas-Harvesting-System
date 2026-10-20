# Yoda's Harvesting System

**A manual and automatic harvesting reflex package for [Achaea, Dreams of Divine Lands](https://www.achaea.com/), using the Nexus client.**

**Version:** 2.0 · **Author:** Master Yoda Darrion, Ancient Acolyte · **Updated:** October 20, 2026

[**Download the latest release**](https://github.com/xeromus79/Yodas-Harvesting-System/releases)

## Overview

Yoda's Harvesting System scans the plants in your current room, identifies supported Harvesting plants, harvests them one at a time, and attempts to store gathered items in your Rift. It includes both **manual harvesting** and **optional automatic harvesting** when you enter a different room.

Automatic mode **does not move your character**. You must navigate from room to room yourself.

## Installation

> [!IMPORTANT]
> **The release package is intentionally distributed disabled.** This is normal. Enable it after importing to display the welcome banner and activate its commands.

1. [Download the `.nxs` package from the latest GitHub release](https://github.com/xeromus79/Yodas-Harvesting-System/releases).
2. Sign in to Achaea using the **Nexus client**.
3. Open **Settings → Reflex Packages** and import the downloaded `.nxs` file.
4. Find **Yoda's Harvesting System** in the package list. It should initially be **disabled**.
5. **Enable** the package. A welcome banner should appear with the available commands.
6. Enter a room containing Harvesting plants and type `hv` to test manual harvesting.

Automatic harvesting remains **off** until you explicitly type `hvon`.

The welcome banner does not normally appear immediately upon import, because the package arrives disabled. It appears when you enable the package, and also when an enabled package loads on a later login or reconnection.

> [!NOTE]
> Avoid keeping multiple active copies of this or other harvesting packages with overlapping aliases and triggers. They can produce duplicate actions or confusing results.

## Commands

| Command | Action |
| --- | --- |
| `hv` | Scan and harvest supported plants in the current room. |
| `hvon` | Enable automatic harvesting when entering a different room. |
| `hvoff` | Disable automatic harvesting for future room entries. |

## How to use

### Manual mode (default)

1. Move to a room with plants.
2. Type `hv`.
3. The system issues `PLANTS`, identifies supported plants, and harvests them sequentially, accounting for balance recovery.
4. When the room's harvest queue is finished, the system stops. Type `hv` again whenever you want another manual scan.

Manual harvesting remains available even when automatic mode is enabled.

### Automatic mode (optional)

1. Type `hvon`.
2. Move to another room **using your normal movement commands**.
3. On entering a room with a different room ID, the system scans for supported plants and attempts to harvest them.
4. Type `hvoff` to prevent new automatic harvests. A harvesting sequence already in progress is allowed to finish.

**Using `LOOK` does not trigger automatic harvesting.** Nexus may issue a room-change event when you look around, but the package compares persistent room IDs and ignores events that do not represent a different room.

**Automatic harvesting starts off whenever the package loads or is re-enabled**, even if it was on before. Enter `hvon` again to resume it.

## How the system works

1. Sends `PLANTS` to inspect the current room.
2. Recognizes supported Harvesting plant identifiers and ignores unrelated resources.
3. Builds a queue of eligible plants without duplicates.
4. Uses Achaea's physical-balance command queue to harvest one plant at a time.
5. After a successful harvest, sends `INR ALL` and waits for balance recovery before proceeding.
6. Skips plants that have been harvested recently, are fully depleted, or cannot be harvested with the character's current skill.
7. Stops once the room's queue is processed.

The system **does not track monthly harvest history** or predict which plants are depleted. It attempts the harvest and responds to Achaea's feedback.

## Supported Harvesting plants

The package recognizes these **24 plant identifiers**:

`ginseng`, `ash`, `echinacea`, `ginger`, `burdock`, `myrrh`, `bellwort`, `bloodroot`, `hawthorn`, `kuzu`, `skullcap`, `slipper`, `goldenseal`, `valerian`, `bayberry`, `cohosh`, `lobelia`, `pear`, `weed`, `irid`, `sileris`, `kelp`, `kola`, `elm`.

Other resources, including items associated with different gathering skills, are ignored.

## Important behavior and limitations

- **`INR ALL` affects all Rift-eligible inventory items**, not only items collected by this package.
- Rapid movement while a scan or harvest sequence is underway has not been exhaustively tested. Allow the current sequence to finish.
- The package depends on specific Achaea output messages and Nexus events. Game or client changes may require updates.
- Harvesting still depends on your character's skills, in-game restrictions, and plant availability.
- `hvoff` stops **new automatic scans**; it does not disable the package or cancel a harvest already underway.
- The package never chooses a destination or issues movement commands for you.

## Troubleshooting

| Problem | What to check |
| --- | --- |
| No welcome banner after importing | The package is intentionally imported disabled. Enable it under **Settings → Reflex Packages**. |
| `hv`, `hvon`, or `hvoff` is not recognized | Confirm that the package is enabled and its aliases are present. |
| `hv` finds nothing | The room may have no supported plants, or the plants may not currently be harvestable. |
| `LOOK` does not trigger harvesting | Expected: automatic mode reacts to a **different room ID**, not looking again in the same room. |
| Movement does not trigger harvesting | Make sure the package is enabled, type `hvon`, and move to another room. |
| Harvesting continues after `hvoff` | An already-started sequence is allowed to finish. |
| Duplicate messages or harvesting attempts | Check for duplicate packages or overlapping harvesting reflexes. |

## Automation and game rules

Achaea's **HELP 15.8** describes restrictions on certain automated activity. This package does not navigate on its own; automatic harvesting requires player-directed movement into each room. **That alone does not guarantee every use complies with current game rules.** Review the applicable rules and ask Achaea administration if you need clarification.

## Downloads and distribution

Get the installable `.nxs` file and downloadable text instructions from the [**GitHub Releases page**](https://github.com/xeromus79/Yodas-Harvesting-System/releases).

For the intended first-run experience, the maintainer exports the package while it is **disabled**. Nexus has been tested to preserve that state when importing, allowing the user to enable it and receive the welcome banner.

---

*Created by Master Yoda Darrion, Ancient Acolyte.*  
*May your harvests be plentiful and your Rift well stocked.*
