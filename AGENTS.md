# Instructions for AI agents

You are working on a WoW UI addon in this repository. To reason about frame names, APIs, and Blizzard’s UI code, you need a local copy of the Blizzard interface dump. This file tells you how to get that copy with minimal user input, and exactly what to ask the user when their help is required.

---

## Your goal

Have **BlizzardInterfaceCode/** (and optionally **BlizzardInterfaceArt/**) at the root of this repo so you can search and cite them when editing the addon.

---

## Step 1: Check if you already have the dump

- If **BlizzardInterfaceCode/** exists at the repo root, you have the code reference. You can proceed with addon work.
- **BlizzardInterfaceArt/** is optional; only needed if you need to reference art assets. If it’s missing, you can still work with the code dump.

If both (or at least BlizzardInterfaceCode) are present, stop here. Otherwise continue.

---

## Step 2: Get the dump from the game (requires the user)

The dump is created by the WoW client. Only the user can run the game and run the in-game command. You cannot do this step yourself.

**Instruct the user as follows:**

---

**Instructions for you (user):** We need a copy of Blizzard’s interface files so the agent can reference them. Please do the following:

1. **Enable the game console**  
   In the Battle.net app: Game Settings → Additional command line arguments → add **`-console`**. Save and launch WoW.

2. **Open the console at the right time**  
   Stay on the **login screen or character select** (do not log into a character). Press **`** (backtick) to open the console.

3. **Run the export command**  
   In the console, type exactly:
   ```text
   ExportInterfaceFiles code
   ```
   and press Enter.  
   Optionally, for art assets, also run:
   ```text
   ExportInterfaceFiles art
   ```

4. **Tell the agent where the files are**  
   The game creates two folders inside your WoW install directory: **BlizzardInterfaceCode** and (if you ran the art command) **BlizzardInterfaceArt**.  
   Reply with the **full path to your WoW install directory** (or the full path to the folder that contains `BlizzardInterfaceCode`).  
   Example (Windows): `C:\Program Files (x86)\World of Warcraft\_anniversary_`  
   Example (macOS): `/Applications/World of Warcraft/_anniversary_`

If the console says “Unknown command,” your WoW build may not support it; the TBC Anniversary client does.

---

## Step 3: Copy the dump into the repo (you do this, using the path from the user)

Once the user has run the export and given you the path to the WoW install (or the parent of `BlizzardInterfaceCode`), you can copy the folders into the repo yourself.

- **Source:**  
  `{path from user}/BlizzardInterfaceCode`  
  and, if they ran the art command:  
  `{path from user}/BlizzardInterfaceArt`

- **Destination:**  
  Root of this repository, so that you end up with:
  - `BlizzardInterfaceCode/`
  - `BlizzardInterfaceArt/` (optional)

Run the appropriate copy command for the environment (e.g. `cp -r` on Linux/macOS/WSL, `Copy-Item -Recurse` in PowerShell, or equivalent). Use the path the user provided; handle spaces and special characters in the path (e.g. quoting) as required by the shell.

After copying, **BlizzardInterfaceCode/** is your main reference for frame names, APIs, and structure. **BlizzardInterfaceArt/** is optional and only present if the art export was run and copied.

---

## When the user asks “how do I dump the API reference?”

Tell them to run **`ExportInterfaceFiles code`** (and optionally **`ExportInterfaceFiles art`**) in the WoW engine console (backtick at login/character-select, with `-console` in launch options), then to give you the path to their WoW install so you can copy the resulting **BlizzardInterfaceCode** (and **BlizzardInterfaceArt**) into the repo. You can use the “Instructions for you (user)” block above as the text you send them.
