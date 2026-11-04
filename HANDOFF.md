# Handoff for a new chat

Read this first. It summarizes the project so far so a new conversation can continue.

## Repository
- GitHub: `calcazarb-cloud/gamechanger`, branch `zero-siege-prototype`.
- Language with the user: Spanish. Short, direct answers. The user follows on a phone in landscape inside the Claude app viewer (game area is about 667x250 CSS px).
- Concept art is generated with Higgsfield (`gpt_image_2_5`, about 0.5 credits per medium image, about 73 credits left). Batches of more than about 5 images hit a rate limit: send them in groups of 4 or 5.

## Active project: "Mitos" (working name), a mobile real-time strategy game
- Folder: `estrategia/`
  - `estrategia/prototype/index.html` plus `estrategia/prototype/assets/`: playable browser prototype.
  - `estrategia/concept-art/`: civilizations, town across ages, maps, units, sprites.
- Published prototype: https://claude.ai/artifact/DVcMQNPisX9hL7jgFcfCdt
- Design document (Claude Docs): https://claude.ai/artifact/2kQCRJw1wEaLj3NjiFb3aS
- Ideas gallery (civilizations, troops, animations, Bronze vs Iron buildings, proposed troops): https://claude.ai/artifact/1ykudfU59gz41xxYQpAdrT
- Decisions so far:
  - 70% Age-of-Empires-style economy and ages, 30% StarCraft-style action.
  - Historical realism with a touch of magic. Three fictional civilizations: Imperio Áureo (Rome and Byzantium), Clanes de la Estepa (steppe horse peoples), Reino de las Arenas (ancient Egypt).
  - Modes: quick match starting in age 2 or 3 (8 to 12 min) and classic match from zero (20 to 30 min). Computer opponent to learn, then 1v1 online, later 2v2 and free-for-all.
  - Villagers work on their own from an economic plan (food, wood, gold, build sliders) with an optional assistant, priority zones and drop-off camps.
  - Money: free game; sells civilizations, campaigns, a season pass and cosmetics; never pay-to-win.
  - Name "Myth" is taken (Bungie RTS, 1997); "Mitos" is provisional.
- Prototype state (quick match vs computer, Bronze Age start):
  - Landscape layout, two-column command rail on the right, compact resource bar, minimap bottom left, UI scales with screen height.
  - One finger pans and two fingers zoom; "Área" toggle for box select; tap to select, double tap selects all of a type, tap the map to command.
  - Buildings: town center, house, farm, lumber camp, mining camp, barracks. Units: villager, spearman, archer, cavalry, legionnaire (Iron Age).
  - Advance to the Iron Age, counter system, town center arrows, computer that builds, advances and attacks in waves.
  - Readability: team discs and glow on units, minimum on-screen size, dimmed map.
- Animations (2026-11-04): painted sprite sheets generated with Higgsfield (gpt_image_2_5, medium, transparent
  background, the concept sprite as reference): `assets/<unit>-anim.webp`, 8 cells in a row (4 walk + 4 attack/work).
  Cell size and foot anchor live in `SHEET` in index.html; on-map height in `DH`. Death is a fall-and-fade of a
  walk frame. Raw generated sheets are in `concept-art/generados/`. The slicing script (alpha components -> cells,
  feet aligned, body height 150 px) is described in the commit; regenerate the sheet and re-slice if a unit changes.
- Ages change the look (2026-11-04): in the Iron Age every building uses its `*3.webp` version (stone and red tile
  roofs) and spearmen and archers switch to iron gear (`spear3`, `archer3` sheets, `UT3` stats: more hp and damage),
  including units already on the map.
- Defense towers (2026-11-04): `tower` building (100 wood, 50 gold), shoots arrows (range 215; stronger in the Iron
  Age, wooden tower becomes a stone tower). The computer also builds up to 2-3 towers.
- Higgsfield: about 64 credits left after this round (each medium 1k image costs 0.5).
- Terrain (2026-11-04): a 168x94 navigation grid (`NAV`, 16 world units per cell) traced from map-h.jpg: water and
  dense painted forest are blocked. The river can only be crossed at the two painted fords (top around map 700,165
  and bottom around 690,615). Units path with A* (`findPath`) and walk straight when the line is clear; buildings
  cannot be placed on blocked cells; choppable trees sit on the forest edges. If map-h.jpg changes, the grid must be
  regenerated (color threshold on the image, then manual fixes at the fords and the river ends).
- User feedback still open: the game is hard to read and play; asked to improve graphics.
- Agreed next steps:
  1. Done: unit animations (procedural from the sprites).
  2. Done: rivers and forests block movement; cross only at fords.
  3. Done: buildings and soldiers change look with the age; defense towers added.
  4. Second civilization, classic match from zero, tutorial campaign, sound, English.
  5. Online play needs hosting outside the artifact (for example Vercel plus Supabase Realtime); ask before creating paid resources.

## Paused project: "Rift Keepers" (hero, base and duels)
- Folder: `rift-keepers/` (prototype, concept art, design doc https://claude.ai/artifact/EDCJdesdrvcqPy79wtqrzD, prototype https://claude.ai/artifact/Cn4jHzXDWfQ94Q5Z2WuqdR).
- Paused by the user in favor of the strategy game; keep it intact.

## Earlier experiments
- `zero-siege/` (math tower defense) and `glimmerkeep/` (tower defense). The user found them boring.
