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
- Animations (2026-11-04): walk (6 frames), attack (4), work (4), idle and a falling death, built at load time
  from each unit sprite (`buildAnim` in index.html: legs split at the hip and swung, upper body leans and swings).
  Melee damage lands on the strike frame and arrows leave on the release frame. Generated per-frame art with
  Higgsfield is still possible later: that needs the user's OK because it spends credits.
- Terrain (2026-11-04): a 168x94 navigation grid (`NAV`, 16 world units per cell) traced from map-h.jpg: water and
  dense painted forest are blocked. The river can only be crossed at the two painted fords (top around map 700,165
  and bottom around 690,615). Units path with A* (`findPath`) and walk straight when the line is clear; buildings
  cannot be placed on blocked cells; choppable trees sit on the forest edges. If map-h.jpg changes, the grid must be
  regenerated (color threshold on the image, then manual fixes at the fords and the river ends).
- User feedback still open: the game is hard to read and play; asked to improve graphics.
- Agreed next steps:
  1. Done: unit animations (procedural from the sprites).
  2. Done: rivers and forests block movement; cross only at fords.
  3. Buildings change look with the age.
  4. Second civilization, classic match from zero, tutorial campaign, sound, English.
  5. Online play needs hosting outside the artifact (for example Vercel plus Supabase Realtime); ask before creating paid resources.

## Paused project: "Rift Keepers" (hero, base and duels)
- Folder: `rift-keepers/` (prototype, concept art, design doc https://claude.ai/artifact/EDCJdesdrvcqPy79wtqrzD, prototype https://claude.ai/artifact/Cn4jHzXDWfQ94Q5Z2WuqdR).
- Paused by the user in favor of the strategy game; keep it intact.

## Earlier experiments
- `zero-siege/` (math tower defense) and `glimmerkeep/` (tower defense). The user found them boring.
