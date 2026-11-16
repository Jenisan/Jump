# Jump

A side-scrolling platformer for the Jenisan Arcade, built on the classic run-and-jump formula (all characters and art are original). Play at **arcade.jenisan.com/jump/** (or jump.jenisan.com).

You play Pip, a jumper in an orange cap and yellow scarf. Run and leap through three worlds (The Outskirts, The Undercity, The Foundry), three levels each, then the loop repeats harder. Every run generates fresh levels.

## Gameplay
- **Hearts and lives.** You have 3 hearts (up to 6 with upgrades) and 3 extra lives. Enemies and spikes cost a heart; pits and running out of time cost a life. Extra life every 20,000 points.
- **Stomp** most enemies from above; chained stomps without touching the ground score more. Sawblades can't be stomped and must be shot.
- **Crates (?)** give coins, items, ammo or a new weapon. Bricks break when you bump them from below.
- **Checkpoint** flag halfway through each level; the **beacon** pole at the end: the higher you grab it, the bigger the bonus, then leftover time is counted into your score.
- **Enemies:** scrap crawlers, spiky crawlers (can't be stomped: shoot them), sparking crawlers (fast; every couple of seconds they throw a shock that hurts anyone close, even from above), wrecked crawlers (look like a scrap pile until you get close, then spring up and chase you), spring bots, soot drones, sawblades, steam turrets and, in the Undercity, hydraulic crushers that drop from the ceiling.

## Weapons (Q / E to switch)
| Weapon | How it works |
|---|---|
| Sling | Pebbles in a short arc. Unlimited. |
| Boomerang | Cuts through every enemy in its path and comes back. One in the air at a time. |
| Fire Wand | Bouncing fireballs, 2 damage. Uses charges. |
| Bombs | Lobbed; the blast does 3 damage, breaks bricks and opens crates. |

## Inventory
The bag holds 2 items (up to 5 with upgrades). Pick a slot with V or 1–5 (or tap it on the HUD) and use it with C. **I** (or Tab, the 🎒 button, or Select on a controller) opens the inventory screen, where you can equip weapons and use or drop items.

| Item | Effect |
|---|---|
| Heart Snack | Restores one heart. |
| Bubble Shield | Blocks the next hit (15 s). |
| Feather | 15 s: one extra air jump, hold jump to glide. |
| Coin Magnet | 15 s: pulls in nearby coins. |
| Ember Pepper | 8 s: faster, and you burn through enemies on contact. |

## Workshop
Coins are banked when a run ends and spent between runs: Big Heart, Spring Boots (double then triple jump), Bigger Bag, Sling Mods, Ammo Pouch, Starter Kit. Three levels each. Save key `jump.save`, settings `jump.settings`.

## Controls
- **Keyboard:** ← → / A D move · Space, ↑, W, Z or K jump (hold for higher) · X, J or Shift fire · Q / E weapon · C use item · V or 1–5 pick item · I inventory · ↓ drop through planks · P / Esc pause · M mute.
- **Controller:** stick / D-pad move · A jump · X or B fire · Y use item · LB / RB weapon · LT / RT pick item · Select inventory · Start pause.
- **Phones and tablets** (landscape only): ◀ ▶ ▼ on the left; JUMP, FIRE, ⟳ (next weapon) and ITEM on the right.

## Files
- `index.html`: the whole game.
- `tiles.webp`: block tiles cut from the supplied block sheet (64 px cells; table `THEMES[].tile` and `TC`; last cell is the plank strip). Each world has its own top, fill, brick and stone tiles; crates are the hazard panel with a live "?".
- `bg.jpg`: the supplied factory skyline, mirrored into a seamless strip; The Outskirts uses it as is, The Foundry tints it fire orange. The Undercity's cavern is drawn in code.
- `ui.webp` (`UIR`) and `ui-panel.webp`, `ui-hazard.webp`, `ui-card.webp`, `ui-card-on.webp`, `ui-btn.webp`: cut from the supplied UI sheet. Panels and cards are 9-slice frames; the HUD uses the heart, coin stack, rust plate (weapon), square plates (bag slots), the gauge bar (time; its channel `BAR_CH` is repainted and filled live) and hazard stripes (banners). Live numbers are always drawn on top.
- `splash.jpg`: key art for the arcade hub card, rendered from the game with `?splash`.
- `soundtrack.mp3`: chiptune loop, levelled to −14 LUFS like every arcade track.
- `sprites.webp` (`SPRR`: x, y, w, h, anchor x, anchor y): painted enemy frames cut from supplied sprite sheets. Scrap crawler: `cw0`–`cw4` walk, `csq` squashed, `cfl` knocked over; drawn 36 units wide, collision box 28×24. Soot drone: `dr0`/`dr1` rotor hover, `drs` parked (rotor stopped); 40 units wide, anchored at the sphere centre. Steam turret: `tu0` idle, `tuc` charging (just before a shot), `tuf` firing flash, `tud` damaged (last hit point), `tux` wrecked; 40 units wide. Hydraulic crusher: `crA` idle head, `crB` slamming head, `rod` tiled from the ceiling `flange` down to the head; head 64 units wide. Pip: `p0` idle, `pr0`–`pr3` run, `pj` jump (also grabbing the beacon), `pf` fall, `ps` throw (0.18 s after each shot), `ph` hurt, `pd` knocked out; drawn 38 units tall, collision box 18×30. Crawler variants: `csp` spiky, `czp` sparking, `cwr` wrecked (also used as the knocked-out frame for all three). Sawblade: `saw`, one disc rebuilt from the clean top half of the supplied blade (the bottom had sparks and a figure overlapping it), spun in code as it rolls, 32 units across. Enemies without painted frames fall back to the code-drawn versions.
- The spring bot, pickups and projectiles (and everything, as a fallback until `sprites.webp` loads) are drawn in code in the same gritty style (dark outlines, rust and steel shading): Pip the steelworker (hard hat, goggles, red bandana, work jacket, tool belt); scrap crawlers, spring bots, soot drones, sawblades (spiky: shoot them) and steam turrets; hydraulic crushers; brass gear coins; hex-nut sling shots.
Version in `VERSION`; bump .01 per shipped build (0.10 first, 0.11 painted UI, tiles and background, 0.12 industrial characters, 0.13 glowing coins with a pickup burst and coins that fly to the HUD counter, 0.14 painted scrap crawler, 0.15 soot drone, 0.16 sawblade, 0.17 steam turret and hydraulic crusher, 0.18 spiky, sparking and wrecked crawlers, 0.19 painted Pip).

## Code map
- `genLevel()`: builds a level from weighted segments (pits, steps, block rows, planks, moving platforms, pillars, spikes, crushers, sentry towers). Tiles: 0 air, 1 ground, 2 brick, 3 crate, 4 used crate, 5 stone, 6 one-way plank, 7 spikes. The attract mode uses pit-free levels.
- `moveBody()`: tile collision (x = centre, y = feet).
- `updatePlayer()`, `updateEnemies()`, `updateProjectiles()`, `updatePickups()`, `updateCrushers()`.
- `fire()`, `useItem()`, `inventory()`, `workshop()`.
- `window.__jump` exposes state for testing.
