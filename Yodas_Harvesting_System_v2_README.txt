YODA'S HARVESTING SYSTEM
Nexus Reflex Package for Achaea, Dreams of Divine Lands
======================================================

Version: 2.0 (Manual + Optional Automatic Harvesting)
Platform: Achaea Nexus Client
Author: Master Yoda Darrion, Ancient Acolyte
Updated: October 20, 2026

OVERVIEW
--------
Yoda's Harvesting System scans the plants in your current room, identifies
supported Harvesting plants, harvests them one at a time, and attempts to
store gathered items in the Rift. Version 2.0 supports both manual
harvesting and optional automatic harvesting when you enter a new room.

INSTALLATION — IMPORTANT: THE PACKAGE ARRIVES DISABLED
------------------------------------------------------
The release package is intentionally exported in a DISABLED state.
This is normal and is part of the installation procedure.

1. Sign in to Achaea using the Nexus client.
2. Open Nexus Settings > Reflex Packages and locate the package import controls.
3. Import the supplied .nxs package.
4. Find "Yoda's Harvesting System" in your Reflex Packages list.
5. ENABLE the newly imported package.
6. A welcome banner should appear, confirming that the package has loaded
   and showing the available commands.
7. Type hv in a room containing Harvesting plants to try manual harvesting.
   Automatic harvesting remains off until you explicitly type hvon.

Do not worry if there is no welcome message at the moment of import:
Nexus does not appear to run the package's onLoad function on initial
import. Enabling the imported, disabled package runs onLoad and displays
the welcome banner. The banner also appears when an enabled package loads
on a subsequent login or reconnection.

IMPORTANT: Avoid installing multiple active copies of this package or
another harvesting package using the same aliases/triggers. Duplicate
package names can also cause confusing behavior during testing.

COMMANDS
--------
  hv      Manually scan and harvest the current room.
  hvon    Enable automatic harvesting upon entering a different room.
  hvoff   Disable automatic harvesting for future room entries.

HOW TO USE IT
-------------
Manual mode (default):
  - Move to a room with plants and type hv.
  - The system requests PLANTS, collects eligible plant names, and
    processes them sequentially.
  - When finished, it stops. Type hv again for another manual scan.

Automatic mode (optional):
  - Type hvon to enable automatic harvesting.
  - Move into another room normally. The system automatically scans
    that new room and harvests eligible plants.
  - Typing LOOK in the same room does NOT trigger a new harvest. Nexus
    may issue a room-change event on LOOK, but the system checks the
    persistent room identifier to avoid false movement detections.
  - The package does not move your character or choose destinations.
  - Type hvoff to stop starting automatic harvests in subsequent rooms.
    An already-started harvesting sequence is allowed to finish.
  - The manual hv command is available regardless of automatic mode.

Automatic harvesting starts OFF when the package loads. If you reconnect,
use hvon again whenever you want to resume automatic harvesting.

WHAT THE PACKAGE DOES
---------------------
  1. Sends PLANTS to inspect the current room.
  2. Recognizes supported Harvesting plant identifiers and ignores
     unrelated resources.
  3. Builds a queue of eligible plants without duplicates.
  4. Uses Achaea's physical-balance queue to harvest plants one at a time.
  5. After a successful harvest, sends INR ALL and waits for balance to
     recover before continuing.
  6. Skips plants that were recently harvested, are fully depleted, or
     cannot be harvested because the required skill is not yet known.
  7. Stops when the current room's queue has been processed.

SUPPORTED HARVESTING PLANTS
---------------------------
ginseng, ash, echinacea, ginger, burdock, myrrh, bellwort, bloodroot,
hawthorn, kuzu, skullcap, slipper, goldenseal, valerian, bayberry,
cohosh, lobelia, pear, weed, irid, sileris, kelp, kola, elm.

Only these 24 identifiers are recognized. Other resources, including
resources from different gathering skills, are ignored.

IMPORTANT BEHAVIOR AND LIMITATIONS
----------------------------------
- INR ALL can store other Rift-eligible inventory items, not just the
  herbs or plants gathered by this package.
- Rapid movement during an active scan or harvest sequence has not been
  exhaustively tested. Allow the current sequence to finish.
- The package relies on specific Achaea messages and Nexus events.
  Changes to the game or client may require updates to its reflexes.
- Harvest success is subject to in-game skills, restrictions, and
  plant availability.
- Disabling the entire reflex package is different from typing hvoff:
  hvoff only prevents future automatic room scans.

TROUBLESHOOTING
---------------
No welcome banner after import:
  The package is intentionally imported disabled. Enable it in the
  Reflex Packages list. The welcome banner should appear then.

The game does not recognize hv, hvon, or hvoff:
  Confirm the package is enabled and that the aliases are present.

Typing hv finds nothing:
  The room may have no eligible Harvesting plants, or its plants may
  already be unavailable for harvesting.

LOOK does not trigger automatic harvesting:
  This is expected. Automatic harvesting detects movement to a
  different room, not a refresh of the current room's description.

Moving does not trigger automatic harvesting:
  Confirm the package is enabled and type hvon. Move to a different
  room to test; LOOK alone will not trigger a scan.

Harvesting continues briefly after hvoff:
  This is expected if a sequence was already underway. hvoff stops
  new automatic scans rather than cancelling the current sequence.

Unexpected duplicate messages, scans, or commands:
  Check for multiple active harvesting packages or duplicated reflexes.
  Keep only one active copy of the system.

AUTOMATION AND GAME RULES
-------------------------
Achaea's HELP 15.8 contains restrictions on certain automated activity.
This package does not navigate on its own: automatic mode requires
player-directed movement into each new room. That design does not, by
itself, establish that every use is permitted. Review the current rules
and seek clarification from Achaea administration if necessary.

DISTRIBUTION
------------
For the intended first-run experience, the maintainer should DISABLE
Yoda's Harvesting System before exporting the release .nxs file.
Nexus has been tested to preserve that disabled state on import.
Include this README with the package, and tell users to ENABLE it after
importing to see the welcome banner and activate the commands.

------------------------------------------------------
Created by Master Yoda Darrion, Ancient Acolyte.
May your harvests be plentiful and your Rift well stocked.
------------------------------------------------------
