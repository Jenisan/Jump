# Jump

A side-scrolling platformer for the Jenisan Arcade, built on the classic run-and-jump formula (all characters and art are original). Play at **arcade.jenisan.com/jump/** (or jump.jenisan.com).

You play Pip, a jumper in an orange cap and yellow scarf. Run and leap through three worlds (The Outskirts, The Undercity, The Foundry), three levels each, then the loop repeats harder. Every run generates fresh levels.

## Gameplay
- **Hearts and lives.** You have 3 hearts (up to 6 with upgrades) and 3 extra lives. Enemies and spikes cost a heart; pits and running out of time cost a life. Extra life every 20,000 points.
- **Stomp** most enemies from above; chained stomps without touching the ground score more. Sawblades can't be stomped and must be shot.
- **Crates (?)** give coins, items, ammo or a new weapon. Bricks break when you bump them from below.
- **Checkpoint** flag halfway through each level; the **beacon** pole at the end: the higher you grab it, the bigger the bonus, then leftover time is counted into your score.
- **Enemies:** scrap crawlers, spiky crawlers (can't be stomped: shoot them), sparking crawlers (fast; every couple of seconds they throw a shock that hurts anyone close, even from above), wrecked crawlers (look like a scrap pile until you get close, then spring up and chase you), spring bots, soot drones, sawblades, steam turrets and, in the Undercity, hydraulic crushers that drop from the ceiling.

## Weapons (toolbar at the bottom: press 1–5, tap a slot, or Q / E to cycle)
| Weapon | How it works |
|---|---|
| Sling | Pebbles in a short arc. Unlimited. |
| Boomerang | Cuts through every enemy in its path and comes back. One in the air at a time. |
| Fire Wand | Bouncing fireballs, 2 damage. Uses charges. |
| Bombs | Lobbed; the blast does 3 damage, breaks bricks and opens crates. |
| Laser Gun | Hold fire for a solid beam (up to ~14 tiles) that stops at the first wall, block or enemy and burns that enemy (about 7 damage a second). Drains 20 cells a second; pickups give 40. Only turns up in crates from world 3-1. |
| Wrench | Close-range swing, 2 damage, smashes bricks and opens crates in front of Pip. Unlimited. Found in crates. |

The toolbar is `G.bar`: five slots (default Sling, Boomerang, Fire Wand, Bombs, Wrench). In the inventory each owned weapon has Toolbar 1–5 buttons to put it in a slot (swapping with whatever was there). A newly found weapon fills the first slot holding a weapon you don't own yet; if there's none, it waits in the inventory. The toolbar shows with their number, ammo counts for the Fire Wand and Bombs, a lock on weapons not found yet, and an orange glow on the selected one.

## Bosses (end of every level)
The beacon is gone. Each level ends in a walled arena: once you're 2 tiles in, a stone gate drops behind you, the camera locks to the arena and the boss arrives. Beat it and the exit door at the far end unlocks and opens; walk in to clear the level (time still counts into the score). Die during the fight and you restart at the arena entrance. Health 16 + 6 per level (capped at level 12); stomping its head does 4 (short cooldown), weapons do their usual damage, the Ember Pepper burns it on contact. Boss down: 5,000 + 1,000 per level, coins, a heart and a fuel can.

Bosses cycle by level (`BORDER`), painted frames in `boss.webp` (`ANB`; 0 idle, 1 wind-up, 2 attack, 3 battered below 35% health and while it blows up):
| Level | Boss | Attacks |
|---|---|---|
| 1, 6, 11… | The Scrap Golem | walks, fist pound (shockwaves both ways), leap slam, charge |
| 2, 7… | The Drill Crawler | drill-first charge (stunned if it hits a wall), drills the floor: shockwaves + flung rocks |
| 3, 8… | The Rust Widow | fast walk, leg stab lunge, leap slam |
| 4, 9… | The Furnace Tank | slow roll, flamethrower cone (wind-up glow first), slag shots |
| 5, 10… | The Hammer Drone | flies above, tracks you, dives hammer-first (shockwaves), slag shots |
Every wind-up shows the wind-up frame with a red glow, so attacks can be read and dodged. Falls back to a code-drawn boss until the atlas loads.

## Gear (worn, chosen in the inventory)
| Gear | Slot | Effect |
|---|---|---|
| Work Boots | Feet | Default. |
| Hyper Boots | Feet | Jump twice as high (jump speed × √2, air jumps too). From crates, world 1-3 on. |
| Jet Pack | Back | Worn from the start with no fuel. Jump again in mid-air (with no air jumps left) and hold jump to fly; thrust 3000, climb 260, burns 55 fuel/s. |
| Turbo Jet Pack | Back | Thrust 3800, climb 390, burns 62 fuel/s. From crates, world 2-2 on. |

Fuel cans (+35, gauge out of 100 in the HUD) replace about one coin in 14 along each level and drop from crates.

**Cheat mode:** Shift+F2 toggles it: every weapon and piece of gear goes into the inventory, and ammo (99 charges, 99 bombs, 999 cells) and fuel stay topped up. Not shown in the help.

## Inventory
The bag holds 2 items (up to 5 with upgrades). Pick a slot with V (or tap it on the HUD) and use it with C. **I** (or Tab, the 🎒 button, or Select on a controller) opens the inventory screen, where you can equip weapons and use or drop items.

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
- **Keyboard:** ← → / A D move · Space, ↑, W, Z or K jump (hold for higher) · X, J or Shift fire · 1–5 select toolbar weapon · Q / E cycle weapon · jump again in mid-air for the jet pack · C use item · V pick item · I inventory · ↓ drop through planks · P / Esc pause · M mute.
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
- `anim.webp` (`ANR`: x, y, w, h, anchor x, anchor y, body height, body width): animated item frames cut from the supplied sheets — `coin0`–`coin3` spin, `snack0`–`snack3` lunchbox (closed, glowing, open, heart pops out; played above Pip when a Heart Snack is used), `shield0`–`shield3` (ring and bubble), `bub1`–`bub3` (the bubble with the ring removed, worn around Pip: forming, steady, crackling in the last 3 s), `feather0`–`feather3`, `magnet0`–`magnet3`, `pepper0`–`pepper3` (pickups loop these), `sling0`–`sling4` (icon, then pull/release/settle shown in Pip's hand after a sling shot), `nut0`–`nut4` spinning sling shot, `boom0`/`boom1`, `heart0`–`heart3` (HUD hearts pulse; the flaming `heart2` flashes when a heart is gained and on heart pickups; empty hearts are greyed). Sized by body height so glows and sparks spill past the item. Second batch: `dust0`–`dust2` (landing/death puffs), `brick0`–`brick3` (brick chunks), `crate0`–`crate3` (in the atlas but unused: the ? blocks from the block sheet are kept for crates), `flag0`–`flag3` (checkpoint: limp/waving grey until reached, then lit orange), `door0`–`door3` (exit door: locked, unlocking, opening, open as Pip walks in after the beacon), `boomfx0`–`boomfx3` (bomb blast), `bomb0`–`bomb3` (fuse burns down while the bomb is in the air), `fball0`/`fball1` (fireball, flipped to its direction), `bcnfull0` (beacon assembled from the supplied base, pipe and lamp head; pole axis at 27.7% of its width), `plat0`–`plat2` (moving platforms; long ones use `plat0`), `wand0`–`wand3` (icon, and lit in Pip's hand after a Fire Wand shot). `anmK()` places a frame by its body box (left, bottom).
- `items.webp` (`ITR`: x, y, w, h): painted coins (`c0`–`c2` spin frames), item icons (`snack`, `shield`, `feather`, `magnet`, `pepper`, `heartx`), weapons (`sling`, `boom1`, `wand`, `bomb`, `ammo` crate), projectiles (`nut`, `fire0`/`fire1`), checkpoint (`cp0` off, `cp1` lit), `beacon`, end `door`, moving platform `plat`, blast frames `e0`–`e2`, dust `d0`/`d1`, brick bits `br0`–`br3`. The wrench icon comes from `ui.webp`.
- The spring bot (and everything, as a fallback until the atlases load) as a fallback until `sprites.webp` loads) are drawn in code in the same gritty style (dark outlines, rust and steel shading): Pip the steelworker (hard hat, goggles, red bandana, work jacket, tool belt); scrap crawlers, spring bots, soot drones, sawblades (spiky: shoot them) and steam turrets; hydraulic crushers; brass gear coins; hex-nut sling shots.
Version in `VERSION`; bump .01 per shipped build (0.10 first, 0.11 painted UI, tiles and background, 0.12 industrial characters, 0.13 glowing coins with a pickup burst and coins that fly to the HUD counter, 0.14 painted scrap crawler, 0.15 soot drone, 0.16 sawblade, 0.17 steam turret and hydraulic crusher, 0.18 spiky, sparking and wrecked crawlers, 0.19 painted Pip, 0.20 painted items and props, weapon toolbar with 1–5 keys, Wrench weapon, 0.21 animated coins, pickups, hearts, shield bubble, snack and sling, 0.22 painted crates, checkpoint flags, beacon, exit door, platforms, bombs, fireballs, wand, blasts, dust and brick chunks, 0.23 Laser Gun, Hyper Boots, Jet Pack + fuel cans, Turbo Jet Pack, choosable toolbar slots and worn gear, Shift+F2 cheat mode, 0.24 crates back to the ? blocks, 0.25 cheat moved to Shift+F2, 0.26 boss arena replaces the beacon, 0.27 five painted bosses with their own attacks).

## Code map
- `genLevel()`: builds a level from weighted segments (pits, steps, block rows, planks, moving platforms, pillars, spikes, crushers, sentry towers). Tiles: 0 air, 1 ground, 2 brick, 3 crate, 4 used crate, 5 stone, 6 one-way plank, 7 spikes. The attract mode uses pit-free levels.
- `moveBody()`: tile collision (x = centre, y = feet).
- `updatePlayer()`, `updateEnemies()`, `updateProjectiles()`, `updatePickups()`, `updateCrushers()`.
- `fire()`, `useItem()`, `inventory()`, `workshop()`.
- `window.__jump` exposes state for testing.
