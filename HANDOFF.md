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
- Three playable civilizations (2026-11-04): chosen on the start screen; the computer gets another one at random.
  `CIV` in index.html holds each civ's barracks roster, priest and AI unit mix. Imperio Aureo (legionary, cavalry,
  scorpion, Sun Priestess heals), Clanes de la Estepa (light cavalry, horse archer, clan spearman is faster, wind
  shaman speeds up nearby troops), Reino de las Arenas (khopesh guard, war chariot, desert archer has more range,
  farms give +25% food, Sun Priest burns a group with a beam). Battering ram for everyone (only hits buildings).
  New Temple building trains the priest. Art keys: civ prefix `e-` / `a-` (Imperio has none), `3` = Iron Age.
- Map (2026-11-04): new sharp 4K painted map `assets/map-4k.webp` (same layout: river with two fords), minimap
  `map-mini.jpg`; the navigation grid was re-traced from it (source copy in `concept-art/mapa-4k.jpg`).
- Readability fixes (2026-11-04): attack and work animations slowed down (attack 0.8 s, hit lands on the strike
  frame); units only get a small size boost when zoomed far out (`usc`); buildings exported at about 3.6x their
  on-map width so they stay sharp.
- Higgsfield: 28 credits left (medium 1k image = 0.5, high 4K map = 4.25).
- Computer play (2026-11-04): left click selects (Shift adds), drag to box-select, right click orders (or sets the
  rally point / cancels placement), wheel zoom, arrows/WASD or screen edge to pan. Shortcuts: B build, P plan,
  H city, Q idle villagers, 1-4 groups, Space pause, Esc cancel. UI scales up on big screens; the controls are listed
  on the start screen only on devices with a mouse. Phone controls are unchanged.
- Added (2026-11-04, second round):
  - Walls (`wall`, drawn as a line: tap start, tap end) and gates (`gate`, only the owner passes). Finished walls
    and gates write into the `DYN` grid that pathfinding reads; destroyed ones clear it.
  - Fords are marked as shallow water (NAV value 3): land units and boats both pass there.
  - Dock (`dock`, must touch the river, not on a ford), fishing boats (fish spots in the river, food goes to the
    dock) and war galleys. Boats move only on water.
  - One hero per civ (General Aureo, Gran Khan, Reina del Sol; aura +25% damage) is coded and has art, but is
    switched off (`HEROES=false`) because the user does not want heroes yet.
  - Steppe houses (yurts) can be moved ("Mover yurta").
  - Sound: effects and a calm harp melody synthesized with Web Audio (no files); the note button cycles music+effects
    / effects only / silent. Generated music with Higgsfield costs about 13 credits per 90 s, so it was not used.
  - Tutorial (start screen button): 9 guided steps, the enemy does not attack until it ends.
  - Building placement shows green/red cells; buildings can sit closer. Buildings sit on a soft ground shadow.
  - Train buttons show how many are queued; descriptions appear on hover (mouse) or long press (phone), and the
    tray describes the selected unit or building.
  - Player orders are obeyed: a move order is a plain move (no stopping to fight on the way), so you can pull units
    out of a fight; the group buttons no longer jump the camera to the middle of the map.
- Pace (2026-11-04, user asked for time to build walls and boats): gathering +35%, building +50%, villagers train
  in 12 s, more starting resources (400 food, 450 wood, 220 gold), first enemy wave at 4:30 and 2:15 between waves;
  walls, gates, docks and boats are cheaper and faster.
- Sound (2026-11-04): plus field ambience (wind, birds), select and order sounds per unit type, arrow impacts,
  victory and defeat tunes. Mute with the note button or the M key.
- Map resources (2026-11-04, user feedback: buildings sat on painted forest and loose trees looked pasted on):
  the painted forest itself is the wood. Every forest cell holds 70 wood (`WOOD`); villagers chop edge cells and a
  chopped cell becomes open ground drawn as a clearing with stumps. No more loose tree sprites. The nav grid no
  longer opens fake holes in the forest around bases (`nav3`), and `layoutBase` places each starting building on
  free meadow (lumber camp by the forest, mining camp by the gold, berries near the town). New gold outcrop and
  berry bush sprites (`gold2.webp`, `berry.webp`).
- Menu (2026-11-04): painted icon tiles (`assets/ui-*.webp`: army, infantry, archers, cavalry, area, city, retreat,
  stop, cancel, repeat, age up, move, idle, plan, rally, attack) with short labels and count badges.
- Buildings blend in (2026-11-04): at load `prepArt` colour-grades building sprites toward the map palette,
  builds a soft shadow silhouette (cast down-right) and tints a cloth banner per team; each building stands on a
  trampled-earth decal (`ground.webp`) and carries its team banner (`banner.webp`) instead of a coloured ring.
- Terrain (2026-11-04): a 168x94 navigation grid (`NAV`, 16 world units per cell) traced from map-h.jpg: water and
  dense painted forest are blocked. The river can only be crossed at the two painted fords (top around map 700,165
  and bottom around 690,615). Units path with A* (`findPath`) and walk straight when the line is clear; buildings
  cannot be placed on blocked cells; choppable trees sit on the forest edges. If map-h.jpg changes, the grid must be
  regenerated (color threshold on the image, then manual fixes at the fords and the river ends).
- Units no longer get stuck on buildings (2026-11-05): every building writes its footprint into the `DYN` path grid
  (value 21, `footBld`/`rebuildDyn`), so paths go around buildings; the soft push only nudges at the edge.
- Army stance (2026-11-05): "Ataque" (hunt enemies within ~170) or "Defensa" (hold position, fight only what comes
  within reach, walk back home if pulled away). Toggle tile in the selected-army menu; new units inherit the last
  choice. Explicit attack orders are always obeyed.
- Buildings under construction can be moved or cancelled (refund of the unbuilt part); Steppe yurts can move any time.
- User feedback still open: the game is hard to read and play; asked to improve graphics.
- Agreed next steps:
  1. Done: unit animations (procedural from the sprites).
  2. Done: rivers and forests block movement; cross only at fords.
  3. Done: buildings and soldiers change look with the age; defense towers added.
  4. Done: second and third civilization. Still to do: classic match from zero, tutorial campaign, sound, English.
  5. Online play needs hosting outside the artifact (for example Vercel plus Supabase Realtime); ask before creating paid resources.

## Paused project: "Rift Keepers" (hero, base and duels)
- Folder: `rift-keepers/` (prototype, concept art, design doc https://claude.ai/artifact/EDCJdesdrvcqPy79wtqrzD, prototype https://claude.ai/artifact/Cn4jHzXDWfQ94Q5Z2WuqdR).
- Paused by the user in favor of the strategy game; keep it intact.

## Earlier experiments
- `zero-siege/` (math tower defense) and `glimmerkeep/` (tower defense). The user found them boring.
