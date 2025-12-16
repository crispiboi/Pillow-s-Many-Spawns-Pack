## Pillow's Many Spawns Pack — content rules

### Directory structure
- Each mod keeps parallel `common` and `42` trees. Always add translations and map assets under both when applicable (e.g., `Contents/mods/<Mod Name>/42/media/lua/shared/Translate/EN/...`).
- Map definitions live under `42/media/maps/<MapName>` with `map.info`, `spawnpoints.lua`, and the shared `RandomOrAnywhere.bik` link (if present).
- Mod metadata: `42/mod.info` (and future 43/44, etc.) must use the workshop id form `1911132112/<ModName>` and `pzversion=42` (or the target version). Root `mod.info` can keep the legacy id for local use, but 42+ must match the workshop id.

### Translation files (title/description)
- Keep `title.txt` as plain text only (no markup). Naming patterns:
  - By Location: `Random Spawns - By Location - <Location>`
  - Anywhere But: `Random Spawns - Anywhere But - <Location>`
  - Variations: `Random Spawns Variations - <Variant>`
  - By Profession: `Random Spawns - By Profession`
  - Louisville Neighborhoods: `Random Spawns - Louisville Neighborhoods - <Neighborhood>`
- `description.txt` uses two lines, separated by newlines:
  ```
  <CENTRE> <SIZE:medium> <HEADING IN CAPS> <LINE> <LINE>
  <LEFT> <SIZE:small> <Body sentence(s)...> <LINE> <LINE>
  ```
  Rules:
  - There must be a space before every `<LINE>` tag (e.g., `... WORD <LINE>`), or the game will mis-parse the string.
  - Use `<HEADING IN CAPS>` that mirrors the title intent (e.g., `RANDOM SPAWNS - LOUISVILLE NEIGHBORHOODS - AUDOBON`).
  - Body text should include the approximate spawn count when known, e.g., `There are approximately 58 locations.`
  - Keep content duplicated in both `common` and `42` translation folders for that entry.
- For Anywhere But, the translation folder name must match the map folder exactly (`Anywhere But - <Location>`) and map.info must reference that exact path.

### Map info files
- `map.info` should reference translation files:
  ```
  title=media/lua/shared/Translate/EN/<Name>/title.txt
  description=media/lua/shared/Translate/EN/<Name>/description.txt
  ```
  (Blank `description=` lines that follow are kept as-is by the existing files.)
- Set `zoomX` and `zoomY` to the average of all spawnpoints:
  - Compute tile coordinates as `tileX = worldX * 300 + posX` and `tileY = worldY * 300 + posY`, then average across all entries in `spawnpoints.lua`.
  - Keep `zoomS` as defined: use 14.5 for Louisville Neighborhoods (or other zoomed-in regions) and 2 to show the full map elsewhere.
  - Update per-neighborhood/area map folders accordingly.
- Map folder names must align with translation folder names (e.g., `Anywhere But - <Location>` must have translations under `Translate/EN/Anywhere But - <Location>`).

### Spawnpoints and counts
- Spawn counts displayed in descriptions should come from the number of `worldX` entries in `spawnpoints.lua` for that map.
- For Louisville Neighborhoods, use the averaged `zoomX/zoomY` per neighborhood (see above) and include the count in the description.

### Spacing and formatting gotchas
- Always ensure a trailing space before `<LINE>` markers in descriptions.
- Keep ASCII-only text unless a file already uses non-ASCII characters.
- Mirror changes into both `common` and `42` translation folders to avoid missing-localization issues.

### Regeneration inputs (reference)
- B42 spawn data originates from `projectzomboidmapping.ods` and the regeneration logic documented in `B42-update-summary.md`. Rebuilds should follow that sheet’s filters and category rules when updating `spawnpoints.lua` files.
