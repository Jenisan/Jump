# Jump

A side-scrolling platformer for the Jenisan Arcade, built on the classic run-and-jump formula (all characters and art are original). Play at **arcade.jenisan.com/jump/** (or jump.jenisan.com).

You play Pip, a jumper in an orange cap and yellow scarf. Run and leap through three worlds (Sunny Meadow, Crystal Caverns, Sunset Skyway), three levels each, then the loop repeats harder. Every run generates fresh levels.

## Gameplay
- **Hearts and lives.** You have 3 hearts (up to 6 with upgrades) and 3 extra lives. Enemies and spikes cost a heart; pits and running out of time cost a life. Extra life every 20,000 points.
- **Stomp** most enemies from above; chained stomps without touching the ground score more. Burrs are spiky and must be shot.
- **Crates (?)** give coins, items, ammo or a new weapon. Bricks break when you bump them from below.
- **Checkpoint** flag halfway through each level; the **beacon** pole at the end: the higher you grab it, the bigger the bonus, then leftover time is counted into your score.
- **Enemies:** beetles, hoppers, bats, burrs, sentries (stone turrets) and, in the caverns, crushers that drop from the ceiling.

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
Single `index.html`, plus `splash.jpg` (key art for the arcade hub card, rendered from the game with `?splash`) and `soundtrack.mp3` (chiptune loop, levelled to −14 LUFS like every arcade track). All game art is drawn in code. Version in `VERSION` (0.10 first); bump .01 per shipped build.

## Code map
- `genLevel()`: builds a level from weighted segments (pits, steps, block rows, planks, moving platforms, pillars, spikes, crushers, sentry towers). Tiles: 0 air, 1 ground, 2 brick, 3 crate, 4 used crate, 5 stone, 6 one-way plank, 7 spikes. The attract mode uses pit-free levels.
- `moveBody()`: tile collision (x = centre, y = feet).
- `updatePlayer()`, `updateEnemies()`, `updateProjectiles()`, `updatePickups()`, `updateCrushers()`.
- `fire()`, `useItem()`, `inventory()`, `workshop()`.
- `window.__jump` exposes state for testing.
