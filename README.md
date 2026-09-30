# HOLLOWMAW (Warden.)
run.

A level-based WebXR horror game with Gorilla-Tag-style arm locomotion. You are a small legless creature; **THE WARDEN**, a 12 m starved giant, hunts you by sound and sight across six levels.

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
| Left trigger | Flashlight. The battery drains, and the light makes you easier for the Warden to see. |
| Grip | Grab and turn valve wheels; curls your fingers. |
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
| 1–6 | Jump to level 0–5. |
| G | God mode (can't be caught, fly with Q/E). |
| C | Show colliders. |
| M | Warden state label and vision cone. |
| P | FPS and draw calls. |

## Levels

0. **The Playground** – tutorial, menu board, light the treehouse lantern. A giant walks past on the horizon.
1. **The Drains** – turn 3 valve wheels. It walks on the street above you and stomps where it hears noise.
2. **The Canopy** – ring 3 bells (they're loud) to open the gate. It walks among the trees and looks up.
3. **The Mill** – find 4 fuses for the generator to power the lift. It crawls in on all fours and reaches into vents.
4. **The Well** – climb 60 m out of the shaft. It comes down the wall head-first to meet you.
5. **The Escape** – rooftop chase under a red moon to the lighthouse gate. Roofs collapse behind you, then the ending plays.

Each level has lantern checkpoints and one hidden carved toy. Progress, toys and settings are saved in `localStorage`.

## CONFIG values most worth tweaking (top of the script)

- **Movement feel:** `JUMP_MULTIPLIER` (1.15), `MAX_JUMP_SPEED` (6.5), `VELOCITY_LIMIT` (0.3), `VELOCITY_HISTORY` (6 frames), `GRAVITY`, `AIR_DRAG`, `GROUND_FRICTION`.
- **Grip:** `RELEASE_DIST` (0.03), `FAST_RELEASE_SPEED`, `UNSTICK_DIST`, `HAND_CONTACT_MARGIN`, `MAX_ARM_LENGTH` (1.0).
- **Body size:** `BODY_RADIUS`, `BODY_OFFSET_Y` (how low you "sit"), `HAND_RADIUS`.
- **Surfaces:** `SURFACES.*` sets `bodyGrip`, `handGrip`, `launch`, `release` and noise per surface. `CRUMBLE_TIME` sets how fast crumbling ledges give way.
- **The Warden:** `WARDEN.VISION_FOV_DEG`, `VISION_RANGE`, `HEAR_THRESHOLD`, `ARM_REACH`, `GRAB_RADIUS`, `REACH_SPEED`, `LOSE_SIGHT_TIME`. Per-level speed, hearing and search time live in each level's `warden` block.
- **Falling / flashlight:** `FALL_RESET_HEIGHT` (Well), `FLASH_DRAIN_PER_SEC`, `FLASH_INTENSITY`.
- **Performance:** `XR_FRAMEBUFFER_SCALE` (0.9), `XR_FOVEATION`, `TEX_SIZE`, `MAX_DUST`, `LIGHT_SCALE`.

## What was verified (headless Chromium, desktop mode)

- **Every level:** loads with no console errors, uses 22–75 draw calls, and plays through its objective to the next level, up to the ending and the "YOU ESCAPED" panel.
- **Arm locomotion** (scripted hand motion at a fixed 72 Hz):
  - resting on your hands holds you up
  - push-jump, swing-jump (about 4 m/s) and arm-running (about 2 m/s) all work
  - hand-over-hand wall climbing works
  - hands stop at walls instead of passing through them
- **The Warden's full loop:** it spots you, hunts, reaches around obstacles, grabs, and the catch sequence plays. You respawn at your last lantern while it resets far away. Hiding deep in a vent keeps you safe while it gropes at the duct.
- **The rest:** menu buttons pressed by hand, settings, level-select locking, pause, snap turn, crumbling ledges, the rooftop chase (rubber-banding and collapsing roofs) and the Web Audio graph.

**Not verified:** anything that needs a real headset. That covers how the movement actually feels, controller-to-hand alignment, haptics and the frame rate on Quest 3S, so tune the CONFIG values above in the headset.
