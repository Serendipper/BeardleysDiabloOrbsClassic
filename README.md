# Beardley's Diablo Orbs – Classic

**This project was vibe-coded.** The TBC Anniversary update was implemented with AI-assisted editing against the in-game API and Blizzard interface code. In practice it runs smoothly; bug reports and patches are welcome.

---

A WoW UI overhaul for **WoW Classic** (including the TBC Anniversary client). Diablo-style orbs for health/power, reworked action bars, and repositioned default UI elements.

- **Original addon:** [Kulturnilpferd/BeardleysDiabloOrbsClassic](https://github.com/Kulturnilpferd/BeardleysDiabloOrbsClassic) (c)2019 Kulturnilpferd  
- **This fork:** Updated for the **TBC Anniversary** release (Interface 20506).

**Maintaining with an AI agent?** See [AGENTS.md](AGENTS.md) for instructions aimed at AI assistants (Cursor, Copilot, etc.) so you can use your own agent to work on this repo with minimal setup.

---

## Changes for TBC Anniversary (this update)

All edits target the new TBC Anniversary build. Summary of what was changed:

### Addon metadata (`BeardleysDiabloOrbsClassic.toc`)
- **Interface:** Set to `20506` for the current TBC Anniversary client (2.5.6).
- **Notes:** Clarified “for Classic WoW (retail)” to match the launcher/client.

### Experience & reputation bars
- **Legacy clients:** Still supports `MainMenuExpBar` and `ReputationWatchBar` when present.
- **Anniversary client:** Uses the unified status bar system:
  - `StatusTrackingBarManager` – primary handler for XP/rep bar.
  - `MainStatusTrackingBarContainer` – fallback when the manager name differs.
- **Layout fix:** Blizzard’s `UpdateBarVisuals()` resets the manager scale on every UIParent layout pass. The addon hooks that and re-applies scale/position, and forces standalone XP/rep border art (MainMenuBar dwarf chrome is hidden by this UI).
- Positioning uses `placeStatusTrackingBars()` / `handleExpReputationBars()` so the bar sits with the Diablo action bar art.

### Action bar & paging
- **Page number:** Support for Anniversary’s `MainActionBar` and `MainActionBar.ActionBarPageNumber`; hides or zeros the page number text instead of relying on older `MainMenuBarPageNumber` / `MainMenuBarArtFrame.PageNumber`.
- **Page buttons:** `ActionBarUpButton` / `ActionBarDownButton` resolved via `MainActionBar.ActionBarPageNumber` when the top-level names differ.
- **Multi-bars:** `VerticalMultiBarsContainer` hooked for the Anniversary layout where used.

### Casting bar
- **Frame name:** Uses `PlayerCastingBarFrame` when present (Anniversary), otherwise falls back to `CastingBarFrame`.

### Micro buttons & bags
- **Guild:** `GuildMicroButton` (Guild & Communities) supported alongside or instead of `SocialsMicroButton`.
- **Help:** `HelpOpenWebTicketButton` included for positioning and scale where it exists.
- **Keyring:** All references guarded with `if (KeyRingButton)` for clients that have it.

### Stance bar
- **Extra buttons:** `StanceButton7` and `StanceButton8` supported for specs with more auras (e.g. Paladin) on the Anniversary client.

### General
- **Frame existence checks:** All references to Blizzard frames wrapped in `if (frame)` so the addon degrades cleanly on older or differently built clients.
- **Events & scripts:** Hooks and `OnEvent` handlers updated for `StatusTrackingBarManager` / `MainStatusTrackingBarContainer` / `VerticalMultiBarsContainer` where appropriate (including `hooksecurefunc` on `UpdateBarVisuals` so XP/rep placement survives layout).
---
Works now like a charm.

If something’s broken or a frame name changed again, open an issue and mention your client (e.g. TBC Anniversary, build/interface version). <3
