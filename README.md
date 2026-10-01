# HOLLOWMAW (Warden.)
run.

A level-based WebXR horror game with Gorilla-Tag-style arm locomotion. You are a small legless creature; **THE WARDEN**, a 12 m starved giant, hunts you by sound and sight across nine levels.

**Update 1: The Deeper Dark** adds:
- **Crawlers.** Blind, wall-walking, hand-grabbing.
- **Throwables, hiding spots and flares.**
- **Three new levels:** The Nest, The Flooded Chapel and The Heart, with a true ending.
- **Warden upgrades:** slam, peek, memory and the Hollow Warden.
- **New modes:** Nightmare, Endless Descent and Time Trial.
- **Cosmetics, lore notes and achievements.**

See [PATCH_NOTES_UPDATE1.md](PATCH_NOTES_UPDATE1.md). The changes against v1 are in [UPDATE1_PATCHES.md](UPDATE1_PATCHES.md) as ordered FIND/REPLACE patches.

Everything lives in one file: `index.html`. Every mesh, texture, sound and UI element is generated in code. The only thing it loads is three.js r160 from jsDelivr through an import map, so the headset needs internet access.

## Play it on a Quest 3S

WebXR only runs on a secure origin (HTTPS or `localhost`). Pick one of these:

1. **GitHub Pages (easiest).** In the repo, go to *Settings → Pages → Deploy from a branch*, pick the branch and `/ (root)`. Then open `https://<user>.github.io/<repo>/` in the Quest Browser and press **ENTER VR**.
2. **USB + localhost.** Run `npx http-server -p 8080` in this folder, plug in the headset and run `adb reverse tcp:8080 tcp:8080`. Then open `http://localhost:8080` in the Quest Browser (`localhost` counts as secure).
3. **Wi-Fi tunnel.** Run `npx http-server -p 8080` and `cloudflared tunnel --url http://localhost:8080`, then open the printed `https://…trycloudflare.com` URL on the headset.

On a PC browser, **PLAY ON DESKTOP (DEBUG)** gives you a keyboard-and-mouse test mode.

## Controls

| VR | |
|---|---|
| Arms | The only way to move. Push the ground down to rise, drag it back to move, swing down and back then let go to jump, pull down on walls to climb, slap walls mid-air to catch them. |
| Left trigger | Flashlight. The battery drains, and the light makes you easier for the Warden to see. It also makes Crawlers flinch away, which drains the battery faster. |
| Grip | Grab and turn valve wheels; curls your fingers. Grip near a bottle, can, stone or flare to pick it up; let go mid-swing to throw it. A hand holding something can't grab surfaces. Grip a cord's knot and pull hard to snap it. |
| Shake your arm | Three fast swings: light a flare, or fling off a Crawler that has latched onto your hand. |
| Hiding spots | Touch a locker, wardrobe, barrel or hatch to open it, climb in, and it pulls shut. Push the door to get out. Moving your hands inside makes noise. |
| Right stick | Snap turn, 30° (can be turned off in Settings). |
| Y (left) | Pause panel. |
| Turn your left wrist toward your face | Wrist display: level, objective, progress, toys, battery. |
| Touch buttons with your hand | Main menu board (in the Playground), pause panel, end panel. |

| Desktop (debug) | |
|---|---|
| Click / mouse | Lock the pointer and look around. Clicking a button presses it. |
| WASD, Shift | Move, sprint. |
| Space | Jump. Hold it against a wall to climb. |
| Left / right mouse button | Reach out with the left / right hand (touch, ring bells, crank valves). |
| F | Flashlight. |
| Esc | Pause. |
| X | Shake hands (light a flare, fling off a Crawler). |
| 1–9 | Jump to level 0–8. |
| E | Start Endless Descent. |
| K | Spawn a Crawler in front of you. |
| U | Unlock everything. |
| Alt+W | Raise the water one step (The Flooded Chapel). Plain W is still "walk". |
| G | God mode (can't be caught, fly down/up with Q/Space). |
| C | Show colliders. |
| M | Warden state label and vision cone. |
| P | FPS and draw calls. |

## Levels

0. **The Playground** – tutorial, menu board, light the treehouse lantern. A giant walks past on the horizon.
1. **The Drains** – turn 3 valve wheels. It walks on the street above you and stomps where it hears noise.
2. **The Canopy** – ring 3 bells (they're loud) to open the gate. It walks among the trees and looks up.
3. **The Mill** – find 4 fuses for the generator to power the lift. It crawls in on all fours and reaches into vents.
4. **The Well** – climb 60 m out of the shaft. It comes down the wall head-first to meet you.
5. **The Escape** – rooftop chase under a red moon to the lighthouse gate. Roofs collapse behind you, then the ending plays and the ground behind the gate cracks open.
6. **The Nest** – a cavern full of the Warden's bedding. It sleeps in the middle; steal the 3 glowing stones beside it. Every sound fills its wake meter, which you can hear as its breathing speeds up. Crawlers hang on the walls. Reached through the hole that opens in the Playground after the first ending.
7. **The Flooded Chapel** – the water rises every 60 s. Water is slippery, slows your hands, and drowns you if you stay under. Climb the pews, pillars, organ pipes and bell tower and ring the bell, while the Warden wades the nave.
8. **The Heart** – breathing flesh, pulsing red light, a giant heartbeat. Grip and pull to snap 3 cords while the Warden and a Crawler swarm hunt you; the chamber changes after each cut. Then climb to daylight for the true ending.

Each level has lantern checkpoints, one hidden carved toy and two lore notes (paper planes). Toys unlock cosmetics at the Shelf in the Playground; the board next to the menu shows achievements.

**Modes** (menu board → MODES):
- **Nightmare** (after the true ending): the Hollow Warden, sharper senses, half the lanterns, no batteries.
- **Endless Descent** (after the first ending): seeded procedural floors made of tunnel, room, bridge, vent-maze, shaft and cavern chunks. Each floor brings more Crawlers and a faster Warden; being caught ends the run. Your best floor shows on the menu.
- **Time Trial** (any finished level): the Warden is switched off, a timer shows on your wrist, and your best run plays back as ghost hands.

**Settings** also include arachnophobia mode (Crawlers become glowing blobs), grab mode (hold or toggle) and subtitles for important sounds.

Progress, toys, notes, achievements, cosmetics, records and settings are saved in `localStorage` (save version 2). A v1 save is migrated automatically the first time Update 1 starts, keeping unlocked levels, toys and settings; the v1 key is left untouched.

## CONFIG values most worth tweaking (top of the script)

- **Movement feel:** `JUMP_MULTIPLIER` (1.15), `MAX_JUMP_SPEED` (6.5), `VELOCITY_LIMIT` (0.3), `VELOCITY_HISTORY` (6 frames), `GRAVITY`, `AIR_DRAG`, `GROUND_FRICTION`.
- **Grip:** `RELEASE_DIST` (0.03), `FAST_RELEASE_SPEED`, `UNSTICK_DIST`, `HAND_CONTACT_MARGIN`, `MAX_ARM_LENGTH` (1.0).
- **Body size:** `BODY_RADIUS`, `BODY_OFFSET_Y` (how low you "sit"), `HAND_RADIUS`.
- **Surfaces:** `SURFACES.*` sets `bodyGrip`, `handGrip`, `launch`, `release` and noise per surface. `CRUMBLE_TIME` sets how fast crumbling ledges give way.
- **The Warden:** `WARDEN.VISION_FOV_DEG`, `VISION_RANGE`, `HEAR_THRESHOLD`, `ARM_REACH`, `GRAB_RADIUS`, `REACH_SPEED`, `LOSE_SIGHT_TIME`. Per-level speed, hearing and search time live in each level's `warden` block.
- **Falling / flashlight:** `FALL_RESET_HEIGHT` (Well), `FLASH_DRAIN_PER_SEC`, `FLASH_INTENSITY`.
- **Performance:** `XR_FRAMEBUFFER_SCALE` (0.9), `XR_FOVEATION`, `TEX_SIZE`, `MAX_DUST`, `LIGHT_SCALE`.

**Update 1 (`CONFIG.UPDATE1`):**
- **Crawlers:** `CRAWLER_HEAR_RANGE` (16), `CRAWLER_HEAR_THRESHOLD` (0.55), `CRAWLER_LISTEN_TIME` (1.1), `CRAWLER_LUNGE_RANGE` (3.2), `CRAWLER_SPEED_STALK` (1.1), `CRAWLER_SHAKE_SPEED` (2.2), `CRAWLER_SHAKES_TO_REMOVE` (3), `CRAWLER_SHRIEK_LOUDNESS` (14), `CRAWLER_FLASH_DRAIN`, `CRAWLER_MAX` (10).
- **Throwables:** `THROW_MULTIPLIER` (1.25), `THROW_MAX_SPEED` (14), `GRAB_RADIUS` (0.14), `PROP_NOISE`, `BOTTLE_SHATTER_SPEED` (3.2).
- **Flares:** `FLARE_TIME` (20), `FLARE_REPEL_RADIUS` (6), `FLARE_LURE_LOUDNESS` / `FLARE_LURE_INTERVAL`.
- **Hiding:** `HIDE_CHECK_RADIUS` (12), `HIDE_CHECK_TIME` (2.6), `HIDE_MOVE_NOISE_SPEED` (0.75), `HIDE_MUFFLE`.
- **Water:** `WATER_RISE_INTERVAL` (60), `WATER_RISE_STEP` (1.5), `WATER_HAND_SLOW` (0.35), `WATER_GRAVITY`, `WATER_DRAG`, `DROWN_TIME` (10).
- **The Nest:** `WAKE_PER_NOISE` (0.09), `WAKE_NEAR_RADIUS` (7), `WAKE_NEAR_PER_SEC`, `WAKE_DECAY`.
- **The Heart:** `CORD_PULL_DIST` (0.32), `CORD_PULL_TIME` (1.1), `CORD_MAX_STRETCH` (0.8), `HEART_BPM` (52).
- **Warden:** `SLAM_RANGE`, `PEEK_TIME` (6), `PEEK_CHANCE`, `MEMORY_PATROL_CHANCE` (0.4), the `NIGHTMARE` multipliers, `ENDLESS_SPEED_PER_FLOOR` (0.07) and `ENDLESS_MAX_SPEED_MULT` (1.8).

## What was verified (headless Chromium, desktop mode)

- **Every level:** loads with no console errors, uses 22–75 draw calls, and plays through its objective to the next level, up to the ending and the "YOU ESCAPED" panel.
- **Arm locomotion** (scripted hand motion at a fixed 72 Hz):
  - resting on your hands holds you up
  - push-jump, swing-jump (about 4 m/s) and arm-running (about 2 m/s) all work
  - hand-over-hand wall climbing works
  - hands stop at walls instead of passing through them
- **The Warden's full loop:** it spots you, hunts, reaches around obstacles, grabs, and the catch sequence plays. You respawn at your last lantern while it resets far away. Hiding deep in a vent keeps you safe while it gropes at the duct.
- **The rest:** menu buttons pressed by hand, settings, level-select locking, pause, snap turn, crumbling ledges, the rooftop chase (rubber-banding and collapsing roofs) and the Web Audio graph.

**Update 1, verified the same way:**
- **No breakage:** all ten levels (0–8 and Endless) load with no console errors at 22–80 draw calls, and the full v1 playthrough and locomotion numbers are unchanged.
- **Crawlers:** they hear a slap, listen, lunge and latch onto a hand. That hand can't anchor, three fast swings fling the Crawler off, and its shrieks send the Warden to investigate. They climb walls, flinch from the flashlight beam (draining battery), and arachnophobia mode swaps them for blobs.
- **Throwables:** a thrown bottle flies, shatters, lures the Warden to the landing point and awards BAIT.
- **Hiding:** the locker door pulls shut behind you and the Warden standing outside doesn't see you. In SEARCH it opens the locker and catches you.
- **Water:** it rises on its timer; you sink slowly, drown after 10 s and respawn.
- **The Nest:** stealing the stones without waking it unlocks DEEP SLEEPER.
- **The Flooded Chapel:** the bell opens the roof hatch and starts the final surge.
- **The Heart:** pulling snaps each cord, paths rise and collapse, checkpoints wake up, and the Warden staggers and falls. Then the shaft opens, the sunrise outro plays and the TRUE ENDING panel appears.
- **Warden upgrades:** SLAM collapses a scaffold, PEEK lines its eye up with a window and spots you, and the Nightmare variant switches on and off.
- **Modes and saves:** Endless goes floor → pit → floor, ends the run when caught and saves the best; Time Trial records a time, saves and replays the ghost; v1 saves migrate.
- **Hub and the rest:** the Playground hole leads into The Nest; notes, the shelf, mirror and board, subtitles, the Level 5 crack and every debug key work.

**Not verified:** anything that needs a real headset. That covers how the movement actually feels, controller-to-hand alignment, haptics and the frame rate on Quest 3S, so tune the CONFIG values above in the headset.

## Quest test plan for Update 1

1. **Old save.** Start the game in the Quest Browser with your existing v1 progress and check that level select still shows what you had unlocked.
2. **Playground hub.** Throw a stone at the throwing sign. Climb into the practice locker and check the slat light, muffled sound and loud heartbeat. Check the Shelf and the mirror (equip a fur), read a paper-plane note, and look at the achievements board.
3. **Settings.** Try GRAB: TOGGLE, subtitles and arachnophobia mode, and check they persist after reloading.
4. **The Mill (3).** Throw a bottle across the room and watch the Warden go to it. Light the flare by shaking it. Hide in a locker while it searches. Watch it peek through the east windows while you're on the upper catwalk.
5. **The Nest (6).** To reach levels 6–8 on the headset without replaying, open the page once with `?unlockall` on the end of the URL; that unlocks every level, mode and cosmetic in that browser's save. On desktop, press U instead. Then approach the sleeping Warden quietly, compare cloth and bone surfaces, and listen to its breathing speed up. Get grabbed by a Crawler and shake it off with three fast swings. Check that climbing still feels the same.
6. **The Flooded Chapel (7).** Let the water rise and feel how slow and slippery it is. Climb pews, pillars, organ pipes and the tower, ring the bell and climb out through the roof.
7. **The Heart (8).** Pull each cord until it snaps, watch the level change, survive the swarm, watch the collapse, climb the shaft and check the sunrise.
8. **Modes.** Play Endless floors 1–3, a Time Trial on a short level (race your ghost on the second run), and one Nightmare level.
9. **Performance.** Watch the frame rate throughout with the Quest's performance overlay (on desktop, P shows FPS and draw calls). Watch the Heart (breathing shader and heartbeat light), the Chapel (water plane plus waders) and a busy Endless cavern, and aim for a steady 72 fps.
