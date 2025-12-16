## Pillow's Many Spawns Pack — content rules

### Directory structure
- Each mod keeps parallel `common` and versioned folders (`41`, `42`, etc.). Always add translations and map assets under both. Common can be minimal but should mirror files present in 41/42 when used by the game.
- Map definitions live under `<version>/media/maps/<MapName>` with `map.info`, `spawnpoints.lua`, and `RandomOrAnywhere.bik`.
- Mod metadata: versioned folders use workshop-style ids `1911132112/<ModName>` with correct `pzversion`; 41 uses plain ids.

### Translation files
- `title.txt` plain text. Naming patterns:
  - By Location: `Random Spawns - By Location - <Location>`
  - Anywhere But: `Random Spawns - Anywhere But - <Location>`
  - Variations: `Random Spawns Variations - <Variant>`
  - By Profession: `Random Spawns - By Profession`
  - Louisville Neighborhoods: `Random Spawns - Louisville Neighborhoods - <Neighborhood>`
  - Main pack specials: e.g., `Random Spawns - One Per City`, `Random Spawns - Even Distribution`
- `description.txt` two lines:
  ```
  <CENTRE> <SIZE:medium> <HEADING> <LINE> <LINE>
  <LEFT> <SIZE:small> <Body...> <LINE> <LINE>
  ```
- Must have a space before each `<LINE>`. Translation folder names must match map folder names exactly.

### Map info files
- Reference translations:
  ```
  title=media/lua/shared/Translate/EN/<Name>/title.txt
  description=media/lua/shared/Translate/EN/<Name>/description.txt
  ```
- Keep `fixed2x=true` where used; `zoomS=2` unless a zoomed-in view is needed (e.g., 14.5 for Louisville Neighborhoods).
- Set `zoomX/zoomY` to average tile coords of spawnpoints (tile = world*300 + pos). Map folder names must align with translation folder names.

### Spawnpoints and counts
- Counts in descriptions come from the number of `worldX` entries in `spawnpoints.lua` for that map.
- Ensure special variants (Urban Dwellers, Rural Retreats, Mallrats, Knox County Cabins, Knox County Camps and Cabins, One Per City, etc.) follow the same folder/translation naming patterns above.

### Spacing/formatting
- Always keep spaces before `<LINE>` markers.
- ASCII only unless the file already uses non-ASCII.
- Mirror changes into both `common` and versioned folders to avoid missing-localization issues.

### Regeneration inputs
- B42 spawn data originates from `projectzomboidmapping.ods`; follow documented filters/category rules (see `B42-update-summary.md`) when regenerating.
