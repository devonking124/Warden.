# HOLLOWMAW — UPDATE 1 "THE DEEPER DARK": patches against v1 index.html
Apply these 137 patches in order, top to bottom, to the v1 `index.html` (commit 9503f5d). Every FIND block is unique in the file at the moment you apply it. Applying all of them reproduces the Update 1 `index.html` byte-for-byte (this was checked by script). Brand-new sections (Crawlers, Warden behaviours, Update 1 systems, levels 6-8 + Endless) appear as "NEW SECTION — INSERT AFTER" patches.

## PATCH #1 — HTML / CONFIG: edit: VR: move only with your arms • Left trigger: flashlight • Grip: grab v…

FIND:
```js
  <div id="status">Loading…</div>
  <div class="keys">
    VR: move only with your arms • Left trigger: flashlight • Grip: grab valves • Right stick: snap turn • Y: pause<br>
    Desktop: click to lock mouse • WASD move • Space jump / hold on a wall to climb • Mouse buttons: reach with hands • F flashlight • Esc pause<br>
    Debug (desktop): 1–6 level • G god mode (Q/E down/up) • C colliders • M Warden debug • P fps
  </div>
```
REPLACE WITH:
```js
  <div id="status">Loading…</div>
  <div class="keys">
    VR: move only with your arms • Left trigger: flashlight • Grip: grab valves, cords and things to throw • Shake: light flares, fling off Crawlers • Right stick: snap turn • Y: pause<br>
    Desktop: click to lock mouse • WASD move • Space jump / hold on a wall to climb • Mouse buttons: reach, grab, throw • X shake hands • F flashlight • Esc pause<br>
    Debug (desktop): 1–9 level • E Endless • K spawn Crawler • U unlock all • Alt+W raise water • G god mode (Q/Space down/up) • C colliders • M Warden debug • P fps
  </div>
```

## PATCH #2 — 1. CONFIG: — THE DEEPER DARK. Every new tunable lives in this block.

FIND:
```js
  // --- Catch sequence ---
  CATCH_TIME: 3.4,
};

```
REPLACE WITH:
```js
  // --- Catch sequence ---
  CATCH_TIME: 3.4,

  // =================================================================
  // UPDATE 1 — THE DEEPER DARK. Every new tunable lives in this block.
  // =================================================================
  UPDATE1: {
    // --- saves ---
    SAVE_KEY: 'hollowmaw_progress_v2', OLD_SAVE_KEY: 'hollowmaw_progress_v1', SAVE_VERSION: 2,
    // --- Crawlers (blind, hunt by sound only) ---
    CRAWLER_MAX: 10,                 // live Crawlers at once (instanced, so 10 cost ~4 draw calls)
    CRAWLER_SPEED_IDLE: 0.25,        // m/s along any surface
    CRAWLER_SPEED_STALK: 1.1,
    CRAWLER_SPEED_FLEE: 2.6,
    CRAWLER_HEAR_RANGE: 16,          // noise fades to nothing at this distance (the Warden hears much further)
    CRAWLER_HEAR_THRESHOLD: 0.55,    // perceived loudness needed to notice a noise
    CRAWLER_LISTEN_TIME: 1.1,        // freeze and listen before stalking
    CRAWLER_LUNGE_RANGE: 3.2,        // leaps at a sound you made when this close
    CRAWLER_LUNGE_TIME: 0.55,        // flight time of a lunge
    CRAWLER_CLING_RADIUS: 0.32,      // a lunging Crawler latches onto a hand this close
    CRAWLER_SHRIEK_INTERVAL: 1.0,    // while clinging it shrieks this often...
    CRAWLER_SHRIEK_LOUDNESS: 14,     // ...this loud (the Warden hears it)
    CRAWLER_SHAKES_TO_REMOVE: 3,     // fast swings needed to fling it off
    CRAWLER_SHAKE_SPEED: 2.2,        // hand speed (m/s) that counts as a swing
    CRAWLER_SHAKE_RESET: 0.9,        // swings must come within this many seconds of each other
    CRAWLER_STUN_TIME: 2.2,
    CRAWLER_FLINCH_TIME: 1.6,        // backs away from the flashlight beam this long
    CRAWLER_FLASH_DRAIN: 1 / 60,     // extra battery per second while the beam holds a Crawler
    CRAWLER_GIVE_UP_TIME: 9,         // stalking with no new sound this long -> back to idle
    CRAWLER_BODY_HEIGHT: 0.16,
    CRAWLER_RADIUS: 0.22,
    CRAWLER_SHED_ON_HUNT: 2,         // Crawlers that drop off the Warden's back when it starts a hunt
    // --- throwables & flare ---
    THROW_MULTIPLIER: 1.25,          // throw = averaged hand velocity * this
    THROW_MAX_SPEED: 14,
    GRAB_RADIUS: 0.14,               // grip within this distance of a prop to pick it up
    PROP_RESTITUTION: 0.32,
    PROP_FRICTION: 0.7,              // sideways speed kept on each bounce
    PROP_NOISE: { bottle: 9, can: 7, stone: 4.5, flare: 3 },   // loudness of an impact (lures the Warden)
    PROP_NOISE_MIN_SPEED: 1.2,
    BOTTLE_SHATTER_SPEED: 3.2,
    FLARE_TIME: 20,                  // seconds of red light
    FLARE_SHAKES: 3,                 // shakes to strike it
    FLARE_REPEL_RADIUS: 6,           // Crawlers will not come closer than this to a burning flare
    FLARE_LURE_LOUDNESS: 6,          // a burning flare hisses this loud...
    FLARE_LURE_INTERVAL: 2.5,        // ...this often (the Warden comes to look)
    FLARE_INTENSITY: 9,
    FLARE_DISTANCE: 16,
    // --- hiding ---
    HIDE_ENTER_TIME: 0.5,            // inside this long and the door pulls shut behind you
    HIDE_MOVE_NOISE_SPEED: 0.75,     // moving a hand faster than this while hidden makes noise
    HIDE_MOVE_NOISE: 1.6,
    HIDE_CHECK_RADIUS: 12,           // in SEARCH the Warden opens hiding spots this close to where it lost you
    HIDE_CHECK_TIME: 2.6,            // how slowly it prises a door open
    HIDE_MUFFLE: 0.75,               // 0..1 lowpass on all sound while hidden
    HELD_BREATH_RANGE: 8,
    HELD_BREATH_TIME: 5,
    // --- water (The Flooded Chapel) ---
    WATER_RISE_INTERVAL: 60,         // seconds between rises
    WATER_RISE_STEP: 1.5,            // metres per rise
    WATER_RISE_TIME: 4,              // seconds a rise takes
    WATER_RISE_INTERVAL_FINAL: 15,   // after the bell rings
    WATER_HAND_SLOW: 0.35,           // free hands follow the controller this sluggishly under water
    WATER_DRAG: 2.2,                 // body velocity damping per second under water
    WATER_GRAVITY: 0.25,             // gravity multiplier for a submerged body
    DROWN_TIME: 10,
    // --- The Nest: wake meter ---
    WAKE_PER_NOISE: 0.09,            // wake added per unit of perceived noise
    WAKE_DECAY: 0.012,               // per second
    WAKE_NEAR_RADIUS: 7,             // being this close to its head slowly wakes it
    WAKE_NEAR_PER_SEC: 0.04,
    WAKE_LIGHT_PER_SEC: 0.15,        // shining the flashlight in its face
    // --- The Heart ---
    CORD_PULL_DIST: 0.32,            // pull a cord this far...
    CORD_PULL_TIME: 1.1,             // ...for this long to snap it
    CORD_MAX_STRETCH: 0.8,           // pulling further than this makes your grip slip
    HEART_BPM: 52,
    // --- Warden upgrades ---
    SLAM_RANGE: 10,                  // slams a platform you stand on if it can get this close
    SLAM_RAISE_TIME: 0.9,
    SLAM_DOWN_TIME: 0.32,
    PEEK_TIME: 6,                    // seconds its eye stays at a gap, window or vent
    PEEK_FOV_DEG: 55,
    PEEK_RANGE: 14,
    PEEK_CHANCE: 0.6,
    PEEK_COOLDOWN: 25,
    MEMORY_PATROL_CHANCE: 0.4,       // chance a patrol leg heads for where it last caught you
    NIGHTMARE: { hearing: 1.5, sight: 1.4, sightRange: 1.2, speed: 1.22, reachSpeed: 1.25, searchTime: 1.3 },
    // --- Endless Descent ---
    ENDLESS_SPEED_PER_FLOOR: 0.07,
    ENDLESS_MAX_SPEED_MULT: 1.8,
    ENDLESS_HEARING_PER_FLOOR: 0.05,
    ENDLESS_BASE_CRAWLERS: 2,
    ENDLESS_CRAWLERS_PER_FLOOR: 1,
    // --- Time Trial ghosts, subtitles ---
    GHOST_HZ: 20,
    GHOST_MAX_SECONDS: 900,
    SUBTITLE_TIME: 2.6,
    SUBTITLE_REPEAT: 1.6,
  },
};
const U1 = CONFIG.UPDATE1;

```

## PATCH #3 — 2. UTILITIES: textures

FIND:
```js
    });
  },
};

```
REPLACE WITH:
```js
    });
  },
  // --- UPDATE 1 textures ---
  rock(S) {
    const c = paintCanvas(S, (u, v, o) => {
      const n = fbm(u, v, 6, 5, 191), m = fbm(u, v, 24, 3, 192), s = fbmAniso(u, v, 4, 12, 3, 193);
      let g = 62 + n * 60 + (m - 0.5) * 30 + (s - 0.5) * 20;
      if (m > 0.66) g *= 0.6;
      o[0] = g * 0.92; o[1] = g * 0.88; o[2] = g * 0.82;
    });
    const ctx = c.getContext('2d'); const r = mulberry32(194);
    scratchLines(ctx, S, 14, 'rgba(15,12,10,0.75)', 1.4, 120, r);   // cracks
    stains(ctx, S, 8, 'rgba(40,55,50,0.3)', 10, 40, r);              // damp patches
    return c;
  },
  flesh(S) {
    const c = paintCanvas(S, (u, v, o) => {
      const n = fbm(u, v, 5, 5, 201), b = fbm(u, v, 20, 3, 202);
      let r = 120 + n * 80 + (b - 0.5) * 30, g = 30 + n * 25, bl = 35 + n * 20;
      if (b > 0.64) { r += 40; g += 25; bl += 20; }       // wet sheen
      if (n < 0.36) { r *= 0.55; g *= 0.5; bl *= 0.55; }
      o[0] = r; o[1] = g; o[2] = bl;
    });
    const ctx = c.getContext('2d'); const r = mulberry32(203);
    scratchLines(ctx, S, 30, 'rgba(60,10,30,0.6)', 2.2, 140, r);     // veins
    scratchLines(ctx, S, 40, 'rgba(120,30,60,0.35)', 1.0, 60, r);
    return c;
  },
  cloth(S) {
    return paintCanvas(S, (u, v, o) => {
      const weave = Math.sin(u * Math.PI * 2 * 64) * Math.sin(v * Math.PI * 2 * 64) * 0.5 + 0.5;
      const patch = Math.floor(u * 3) + Math.floor(v * 3) * 3;
      const n = fbm(u, v, 8, 4, 212);
      const g = 70 + n * 50 + weave * 14;
      o[0] = g * (0.8 + hash2(patch, 7, 211) * 0.4); o[1] = g * (0.7 + hash2(patch, 8, 213) * 0.3); o[2] = g * (0.6 + hash2(patch, 9, 214) * 0.3);
    });
  },
  bone(S) {
    const c = paintCanvas(S, (u, v, o) => {
      const n = fbm(u, v, 6, 4, 221), s = fbmAniso(u, v, 2, 24, 3, 222);
      const g = 175 + (n - 0.5) * 50 + (s - 0.5) * 30;
      o[0] = g; o[1] = g * 0.94; o[2] = g * 0.8;
    });
    const ctx = c.getContext('2d'); const r = mulberry32(223);
    scratchLines(ctx, S, 10, 'rgba(70,55,40,0.5)', 1, 70, r);
    stains(ctx, S, 6, 'rgba(110,80,50,0.3)', 8, 30, r);
    return c;
  },
  paper(S) {
    const c = paintCanvas(S, (u, v, o) => {
      const g = 205 + (fbm(u, v, 10, 3, 231) - 0.5) * 30;
      o[0] = g; o[1] = g * 0.97; o[2] = g * 0.88;
    });
    const ctx = c.getContext('2d'); const r = mulberry32(232);
    ctx.strokeStyle = 'rgba(90,110,160,0.35)'; ctx.lineWidth = 1;
    for (let y = 16; y < S; y += 16) { ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(S, y); ctx.stroke(); }
    scratchLines(ctx, S, 12, 'rgba(40,40,60,0.5)', 1.6, 50, r);      // crayon scribbles
    return c;
  },
  furPale(S) { return furCanvas(S, 241, [200, 190, 175], [235, 228, 215], 0); },
  furEmber(S) { return furCanvas(S, 251, [120, 50, 25], [230, 120, 50], 0); },
  furStriped(S) { return furCanvas(S, 261, [120, 92, 64], [50, 38, 30], 4); },
  furMoss(S) { return furCanvas(S, 271, [55, 75, 40], [110, 140, 70], 0); },
  furGhost(S) { return furCanvas(S, 281, [150, 175, 200], [210, 230, 255], 0); },
};
// UPDATE 1: fur variants for the hand cosmetics (same strand painter as 'hair')
function furCanvas(S, seed, base, tip, stripes) {
  const c = paintCanvas(S, (u, v, o) => {
    const n = fbm(u, v, 12, 4, seed);
    let k = 0.55 + n * 0.6;
    if (stripes && Math.sin((u + n * 0.15) * Math.PI * 2 * stripes) > 0.35) k *= 0.45;
    o[0] = base[0] * k; o[1] = base[1] * k; o[2] = base[2] * k;
  });
  const ctx = c.getContext('2d'); const r = mulberry32(seed + 1);
  for (let i = 0; i < 2600; i++) {
    const x = r() * S, y = r() * S, a = -1.2 + r() * 0.5, l = 4 + r() * 7, k = 0.5 + r() * 0.7;
    ctx.strokeStyle = `rgba(${tip[0] * k | 0},${tip[1] * k | 0},${tip[2] * k | 0},0.8)`;
    ctx.lineWidth = 0.8; ctx.beginPath(); ctx.moveTo(x, y); ctx.lineTo(x + Math.cos(a) * l, y + Math.sin(a) * l); ctx.stroke();
  }
  return c;
}

```

## PATCH #4 — 2. UTILITIES: rock:     { tex: 'rock', scale: 4 },

INSERT AFTER:
```js
  cobble:   { tex: 'cobble', scale: 4 },
  plain:    { tex: null, scale: 1 },
};
```
NEW CODE:
```js
  // UPDATE 1
  rock:     { tex: 'rock', scale: 4 },
  flesh:    { tex: 'flesh', scale: 3, breathe: true },   // swells and glows with the Heart
  cloth:    { tex: 'cloth', scale: 1.5 },
  bone:     { tex: 'bone', scale: 1.5 },
  paper:    { tex: 'paper', scale: 1 },
  glow:     { tex: null, scale: 1, basic: true },       // unlit: fungus, gems, windows
```

## PATCH #5 — 2. UTILITIES: living flesh. Vertices swell around a centre point (crack-free: the offset depends only

FIND:
```js
  if (MAT_CACHE.has(key)) return MAT_CACHE.get(key);
  const def = MAT_DEFS[key] || MAT_DEFS.plain;
  const m = new THREE.MeshLambertMaterial({ map: def.tex ? getTexture(def.tex) : null, vertexColors: true });
  m.userData.shared = true;
  MAT_CACHE.set(key, m);
  return m;
}
```
REPLACE WITH:
```js
  if (MAT_CACHE.has(key)) return MAT_CACHE.get(key);
  const def = MAT_DEFS[key] || MAT_DEFS.plain;
  const m = def.basic ? new THREE.MeshBasicMaterial({ vertexColors: true })
    : new THREE.MeshLambertMaterial({ map: def.tex ? getTexture(def.tex) : null, vertexColors: true });
  if (def.breathe) makeBreathing(m);
  m.userData.shared = true;
  MAT_CACHE.set(key, m);
  return m;
}
// UPDATE 1: living flesh. Vertices swell around a centre point (crack-free: the offset depends only
// on world position) and glow red on each heartbeat. One shared program for every flesh mesh.
const FLESH_UNIFORMS = { uBreath: { value: 0 }, uPulse: { value: 0 }, uBreathCenter: { value: new THREE.Vector3() } };
function makeBreathing(m) {
  m.onBeforeCompile = (shader) => {
    Object.assign(shader.uniforms, FLESH_UNIFORMS);
    shader.vertexShader = 'uniform float uBreath;\nuniform vec3 uBreathCenter;\n' + shader.vertexShader.replace('#include <begin_vertex>', `#include <begin_vertex>
      vec4 wpB = vec4(transformed, 1.0);
      #ifdef USE_INSTANCING
        wpB = instanceMatrix * wpB;
      #endif
      wpB = modelMatrix * wpB;
      float swell = sin(uBreath * 1.3 + length(wpB.xz - uBreathCenter.xz) * 0.12);
      transformed += (wpB.xyz - uBreathCenter) * (swell * 0.0025)
        + vec3(sin(uBreath * 2.1 + wpB.y * 0.7 + wpB.z * 0.3), sin(uBreath * 1.7 + wpB.x * 0.6), sin(uBreath * 1.9 + wpB.x * 0.4 + wpB.y * 0.5)) * 0.018;`);
    shader.fragmentShader = 'uniform float uPulse;\n' + shader.fragmentShader.replace('#include <emissivemap_fragment>', `#include <emissivemap_fragment>
      totalEmissiveRadiance += diffuseColor.rgb * vec3(1.1, 0.25, 0.2) * uPulse;`);
  };
  m.customProgramCacheKey = () => 'flesh-breath';
}
```

## PATCH #6 — 3. AUDIO ENGINE: edit: levelTimers: { drip: 0, creak: 0, thud: 0, wind: 0, bird: 0, wet: 0 },

FIND:
```js
  lastImpact: 0,
  levelNodes: [],        // ambience nodes to stop on level unload
  levelTimers: { drip: 0, creak: 0, thud: 0, wind: 0, bird: 0 },
  levelAmb: null,
```
REPLACE WITH:
```js
  lastImpact: 0,
  levelNodes: [],        // ambience nodes to stop on level unload
  levelTimers: { drip: 0, creak: 0, thud: 0, wind: 0, bird: 0, wet: 0 },
  levelAmb: null,
```

## PATCH #7 — 3. AUDIO ENGINE: edit: muffle: null, muffleAmt: 0,

INSERT AFTER:
```js
  music: null,
  distortCurve: null,

```
NEW CODE:
```js
  muffle: null, muffleAmt: 0,
```

## PATCH #8 — 3. AUDIO ENGINE: one lowpass on everything for hiding and being under water

FIND:
```js
    this.comp.attack.value = 0.004; this.comp.release.value = 0.25;
    this.master = ctx.createGain(); this.master.gain.value = this.volume;
    this.master.connect(this.comp); this.comp.connect(ctx.destination);
    this.sfx = ctx.createGain(); this.sfx.connect(this.master);
```
REPLACE WITH:
```js
    this.comp.attack.value = 0.004; this.comp.release.value = 0.25;
    this.master = ctx.createGain(); this.master.gain.value = this.volume;
    // UPDATE 1: one lowpass on everything for hiding and being under water
    this.muffle = ctx.createBiquadFilter(); this.muffle.type = 'lowpass'; this.muffle.frequency.value = 20000; this.muffle.Q.value = 0.5;
    this.master.connect(this.muffle); this.muffle.connect(this.comp); this.comp.connect(ctx.destination);
    this.sfx = ctx.createGain(); this.sfx.connect(this.master);
```

## PATCH #9 — 3. AUDIO ENGINE: 0 = clear, 1 = deep under water. Hiding sits around 0.75.

INSERT AFTER:
```js
  resume() { if (this.ctx && this.ctx.state !== 'running') this.ctx.resume().catch(() => {}); },
  setVolume(v) { this.volume = v; if (this.master) this.master.gain.setTargetAtTime(v, this.ctx.currentTime, 0.05); },
  get now() { return this.ctx ? this.ctx.currentTime : 0; },
```
NEW CODE:
```js
  // UPDATE 1: 0 = clear, 1 = deep under water. Hiding sits around 0.75.
  setMuffle(amount) {
    if (!this.ready) return;
    const a = clamp(amount, 0, 1);
    if (Math.abs(a - this.muffleAmt) < 0.01) return;
    this.muffleAmt = a;
    this.muffle.frequency.setTargetAtTime(20000 * Math.pow(350 / 20000, a), this.now, 0.08);
  },
```

## PATCH #10 — 3. AUDIO ENGINE: base pitch (the chapel bell is an octave down and rings longer)

FIND:
```js
    lfo.connect(lg); lg.connect(o.frequency); lfo.start(t); lfo.stop(t + dur + 0.05);
  },
  bell(pos, vol = 1) {
    if (!this.ready) return;
    const t = this.now, d = this.dest(pos, 6, 0.6);
    const base = 262;
    [0.5, 1, 1.183, 1.506, 2, 2.514, 2.662, 3.011].forEach((r, i) => {
      const g = this.envGain(t, 0.004, vol * 0.22 / (1 + i * 0.3), 5.5 - i * 0.5, d);
      this.osc('sine', base * r, t, 5.5, g);
    });
```
REPLACE WITH:
```js
    lfo.connect(lg); lg.connect(o.frequency); lfo.start(t); lfo.stop(t + dur + 0.05);
  },
  bell(pos, vol = 1, base = 262) {   // UPDATE 1: base pitch (the chapel bell is an octave down and rings longer)
    if (!this.ready) return;
    const t = this.now, d = this.dest(pos, 6, 0.6);
    const L = Math.sqrt(262 / base);
    [0.5, 1, 1.183, 1.506, 2, 2.514, 2.662, 3.011].forEach((r, i) => {
      const g = this.envGain(t, 0.004, vol * 0.22 / (1 + i * 0.3), (5.5 - i * 0.5) * L, d);
      this.osc('sine', base * r, t, 5.5 * L, g);
    });
```

## PATCH #11 — NEW SECTION — 3. AUDIO ENGINE: one-shots

INSERT AFTER:
```js
    const t = this.now, d = this.dest(pos, 1, 1);
    this.noiseBurst(t, 0.35, 'bandpass', 1200, 0.6, vol * 0.5, d, 0.01);
  },
```
NEW CODE:
```js
  },

  // ---------- UPDATE 1 one-shots ----------
  chitter(pos, vol = 0.5) {      // Crawler clicking to itself
    if (!this.ready || !this.claimVoice(0.5)) return;
    const t = this.now, d = this.dest(pos, 1, 1.4);
    const n = 3 + Math.floor(Math.random() * 4);
    for (let i = 0; i < n; i++) {
      const t0 = t + i * (0.04 + Math.random() * 0.05);
      const g = this.envGain(t0, 0.002, vol * 0.25, 0.05, d);
      const o = this.osc('square', 2200 + Math.random() * 1800, t0, 0.05, g);
      o.frequency.exponentialRampToValueAtTime(900 + Math.random() * 600, t0 + 0.045);
    }
  },
  shriek(pos, vol = 1) {         // Crawler shriek: high, ragged, distorted
    if (!this.ready || !this.claimVoice(0.8)) return;
    const t = this.now, d = this.dest(pos, 2, 1), dur = 0.7;
    const ws = this.ctx.createWaveShaper(); ws.curve = this.distortCurve;
    const f = this.ctx.createBiquadFilter(); f.type = 'bandpass'; f.frequency.value = 2600; f.Q.value = 1.2;
    const g = this.envGain(t, 0.01, vol * 0.5, dur, d);
    ws.connect(f); f.connect(g);
    const pre = this.ctx.createGain(); pre.gain.value = 0.5; pre.connect(ws);
    [1180, 1530, 2210].forEach((fr, i) => {
      const o = this.osc(i ? 'square' : 'sawtooth', fr, t, dur, pre);
      o.frequency.setValueAtTime(fr * 0.8, t); o.frequency.exponentialRampToValueAtTime(fr * 1.5, t + 0.12); o.frequency.exponentialRampToValueAtTime(fr * 0.9, t + dur);
      const lfo = this.ctx.createOscillator(); lfo.frequency.value = 23 + i * 7;
      const lg = this.ctx.createGain(); lg.gain.value = fr * 0.06;
      lfo.connect(lg); lg.connect(o.frequency); lfo.start(t); lfo.stop(t + dur);
    });
    this.noiseBurst(t, dur * 0.8, 'highpass', 4000, 0.7, vol * 0.25, d);
  },
  wade(pos, vol = 0.5) {         // a hand breaking the water surface
    if (!this.ready || !this.claimVoice(0.6)) return;
    const t = this.now, d = this.dest(pos, 1, 1);
    const n = this.noiseBurst(t, 0.45, 'lowpass', 900, 0.8, vol * 0.5, d, 0.06);
    n.f.frequency.exponentialRampToValueAtTime(300, t + 0.4);
    this.noiseBurst(t + 0.05, 0.25, 'bandpass', 2200, 1.5, vol * 0.15, d, 0.02);
  },
  bigSplash(pos, vol = 1) {      // the Warden wading
    if (!this.ready || !this.claimVoice(1.6)) return;
    const t = this.now, d = this.dest(pos, 8, 0.6);
    this.noiseBurst(t, 1.4, 'lowpass', 1400, 0.6, vol * 0.8, d, 0.01);
    this.noiseBurst(t + 0.1, 1.0, 'bandpass', 3000, 0.8, vol * 0.25, d, 0.05);
    for (let i = 0; i < 4; i++) {
      const t0 = t + 0.2 + Math.random() * 0.8;
      const g = this.envGain(t0, 0.005, vol * 0.12, 0.12, d);
      const o = this.osc('sine', 300 + Math.random() * 500, t0, 0.12, g); o.frequency.exponentialRampToValueAtTime(900, t0 + 0.1);
    }
  },
  shatter(pos, vol = 1) {        // a bottle breaking
    if (!this.ready || !this.claimVoice(1.2)) return;
    const t = this.now, d = this.dest(pos, 2, 1);
    this.noiseBurst(t, 0.5, 'highpass', 3500, 0.7, vol * 0.7, d, 0.002);
    for (let i = 0; i < 9; i++) {
      const t0 = t + Math.random() * 0.25;
      const g = this.envGain(t0, 0.001, vol * 0.12, 0.3 + Math.random() * 0.4, d);
      this.osc('sine', 2500 + Math.random() * 4500, t0, 0.7, g);
    }
  },
  tink(pos, vol = 0.5, base = 900) {   // a can or bottle bouncing
    if (!this.ready || !this.claimVoice(0.5)) return;
    const t = this.now, d = this.dest(pos, 1.5, 1);
    [1, 2.76, 5.4].forEach((r, i) => {
      const g = this.envGain(t, 0.001, vol * 0.18 / (1 + i), 0.35 - i * 0.08, d);
      this.osc('sine', base * r * (0.95 + Math.random() * 0.1), t, 0.35, g);
    });
  },
  lidCreak(pos, vol = 0.5) { this.creak(pos, vol, 0.7, 160 + Math.random() * 60); },
  flareIgnite(pos) {
    if (!this.ready) return;
    const t = this.now, d = this.dest(pos, 1.5, 1);
    this.noiseBurst(t, 0.6, 'highpass', 1500, 0.6, 0.8, d, 0.005);
    const g = this.envGain(t, 0.002, 0.4, 0.15, d);
    const o = this.osc('square', 180, t, 0.15, g); o.frequency.exponentialRampToValueAtTime(60, t + 0.12);
  },
  heartPulse(pos, vol = 1) {     // The Heart: a huge wet double thump
    if (!this.ready) return;
    const t = this.now, d = this.dest(pos, 14, 0.4);
    [0, 0.24].forEach((off, i) => {
      const g = this.envGain(t + off, 0.012, vol * (i ? 0.7 : 1.1), 0.5, d);
      const o = this.osc('sine', 48, t + off, 0.55, g); o.frequency.exponentialRampToValueAtTime(26, t + off + 0.4);
      this.noiseBurst(t + off, 0.25, 'lowpass', 160, 0.8, vol * 0.5, d, 0.01);
    });
  },
  wetCreak(pos, vol = 0.5) {     // flesh stretching
    if (!this.ready || !this.claimVoice(1.4)) return;
    const t = this.now, d = this.dest(pos, 4, 0.8), dur = 1.2;
    const f = this.ctx.createBiquadFilter(); f.type = 'lowpass'; f.frequency.value = 500; f.Q.value = 5;
    const g = this.envGain(t, 0.15, vol * 0.6, dur, d); f.connect(g);
    const o = this.osc('sawtooth', 70 + Math.random() * 30, t, dur, f);
    o.frequency.linearRampToValueAtTime(45, t + dur);
    this.noiseBurst(t, dur, 'bandpass', 700, 2, vol * 0.2, d, 0.3);
  },
  snapCord(pos) {
    if (!this.ready) return;
    const t = this.now, d = this.dest(pos, 6, 0.6);
    this.noiseBurst(t, 0.15, 'bandpass', 900, 0.8, 1.0, d, 0.002);
    this.noiseBurst(t, 1.6, 'lowpass', 500, 0.7, 0.7, d, 0.02);
    const g = this.envGain(t, 0.005, 0.9, 1.2, d);
    const o = this.osc('sine', 90, t, 1.2, g); o.frequency.exponentialRampToValueAtTime(30, t + 1.0);
  },
  dyingMoan(pos, vol = 1) {      // the Warden's last breath: long, falling, slowing vibrato
    if (!this.ready) return;
    const t = this.now, d = this.dest(pos, 14, 0.4), dur = 8;
    const f = this.ctx.createBiquadFilter(); f.type = 'lowpass'; f.Q.value = 2;
    f.frequency.setValueAtTime(700, t); f.frequency.exponentialRampToValueAtTime(160, t + dur);
    const g = this.envGain(t, 1.2, vol * 0.6, dur, d); f.connect(g);
    [58, 59.2, 87.5, 116].forEach((fr) => {
      const o = this.osc('sawtooth', fr, t, dur, f);
      o.frequency.setValueAtTime(fr * 1.1, t); o.frequency.exponentialRampToValueAtTime(fr * 0.55, t + dur);
      const lfo = this.ctx.createOscillator(); lfo.frequency.setValueAtTime(5, t); lfo.frequency.linearRampToValueAtTime(1.2, t + dur);
      const lg = this.ctx.createGain(); lg.gain.value = fr * 0.04;
      lfo.connect(lg); lg.connect(o.frequency); lfo.start(t); lfo.stop(t + dur);
    });
  },
  birds(around) {                // dawn chorus for the true ending
    if (!this.ready) return;
    const t = this.now;
    for (let k = 0; k < 3; k++) {
      const p = _v8.set((Math.random() - 0.5) * 40, 6 + Math.random() * 10, (Math.random() - 0.5) * 40).add(around);
      const d = this.panner(p, 6, 0.8);
      const t0 = t + k * 0.6 + Math.random() * 0.5, base = 2600 + Math.random() * 1600;
      const n = 3 + Math.floor(Math.random() * 4);
      for (let i = 0; i < n; i++) {
        const ti = t0 + i * 0.11;
        const g = this.envGain(ti, 0.005, 0.08, 0.09, d);
        const o = this.osc('sine', base, ti, 0.1, g);
        o.frequency.exponentialRampToValueAtTime(base * (1.2 + Math.random() * 0.4), ti + 0.05);
        o.frequency.exponentialRampToValueAtTime(base * 0.8, ti + 0.09);
      }
    }
```

## PATCH #12 — 3. AUDIO ENGINE: three skitter voices that follow the three nearest moving Crawlers

INSERT AFTER:
```js
    ho.connect(hf); hf.connect(hg); hg.connect(hp); hp.connect(this.sfx); ho.start();
    this.loops.hum = { gain: hg, panner: hp };
  },
```
NEW CODE:
```js
    // UPDATE 1: three skitter voices that follow the three nearest moving Crawlers
    this.loops.skitter = [];
    for (let i = 0; i < 3; i++) {
      const sn = this.noise(true);
      const sf = ctx.createBiquadFilter(); sf.type = 'bandpass'; sf.frequency.value = 3200 + i * 500; sf.Q.value = 2.5;
      const sg = ctx.createGain(); sg.gain.value = 0;
      const sp = ctx.createPanner(); sp.panningModel = 'HRTF'; sp.distanceModel = 'inverse'; sp.refDistance = 1; sp.rolloffFactor = 1.3; sp.maxDistance = 40;
      sn.connect(sf); sf.connect(sg); sg.connect(sp); sp.connect(this.sfx); sn.start();
      this.loops.skitter.push({ gain: sg, panner: sp });
    }
    // a burning flare's hiss
    const fn = this.noise(true);
    const ff = ctx.createBiquadFilter(); ff.type = 'bandpass'; ff.frequency.value = 2400; ff.Q.value = 0.8;
    const fg = ctx.createGain(); fg.gain.value = 0;
    const fp = ctx.createPanner(); fp.panningModel = 'HRTF'; fp.distanceModel = 'inverse'; fp.refDistance = 1.5; fp.rolloffFactor = 1;
    fn.connect(ff); ff.connect(fg); fg.connect(fp); fp.connect(this.sfx); fn.start();
    this.loops.flare = { gain: fg, panner: fp };
    // rushing water (The Flooded Chapel)
    const rn = this.noise(true);
    const rf = ctx.createBiquadFilter(); rf.type = 'lowpass'; rf.frequency.value = 600; rf.Q.value = 0.7;
    const rg = ctx.createGain(); rg.gain.value = 0;
    rn.connect(rf); rf.connect(rg); rg.connect(this.ambBus); rn.start();
    this.loops.rush = { gain: rg, filter: rf };
  },
  setSkitter(i, vol, pos) {
    const s = this.ready && this.loops.skitter[i];
    if (!s) return;
    s.gain.gain.setTargetAtTime(vol, this.now, 0.012);
    if (pos) this.setPannerPos(s.panner, pos);
  },
  setFlareLoop(vol, pos) {
    if (!this.ready) return;
    this.loops.flare.gain.gain.setTargetAtTime(vol, this.now, 0.1);
    if (pos) this.setPannerPos(this.loops.flare.panner, pos);
  },
  setRush(vol) {
    if (!this.ready) return;
    this.loops.rush.gain.gain.setTargetAtTime(vol * 0.5, this.now, 0.6);
    this.loops.rush.filter.frequency.setTargetAtTime(400 + vol * 900, this.now, 0.6);
```

## PATCH #13 — 3. AUDIO ENGINE: breathRate speeds the Warden's breathing (the Nest wake meter); hide = 0..1 while hidden

FIND:
```js
    });
  },
  updateLoops(dt, fear, wardenHeadPos, wardenActive, wardenBreathVol) {
    if (!this.ready) return;
```
REPLACE WITH:
```js
    });
  },
  // UPDATE 1: breathRate speeds the Warden's breathing (the Nest wake meter); hide = 0..1 while hidden
  updateLoops(dt, fear, wardenHeadPos, wardenActive, wardenBreathVol, breathRate = 1, hide = 0) {
    if (!this.ready) return;
```

## PATCH #14 — 3. AUDIO ENGINE: edit: wb.phase += dt * (0.18 + fear * 0.1) * breathRate;

FIND:
```js
    // Warden breath: slow inhale/exhale
    const wb = this.loops.wBreath;
    wb.phase += dt * (0.18 + fear * 0.1);
    const s = Math.sin(wb.phase * Math.PI * 2);
```
REPLACE WITH:
```js
    // Warden breath: slow inhale/exhale
    const wb = this.loops.wBreath;
    wb.phase += dt * (0.18 + fear * 0.1) * breathRate;
    const s = Math.sin(wb.phase * Math.PI * 2);
```

## PATCH #15 — 3. AUDIO ENGINE: hidden: slow, held breath

FIND:
```js
    // Player breath: speeds up with fear
    const pb = this.loops.pBreath;
    pb.phase += dt * (0.25 + fear * 0.9);
    const ps = Math.sin(pb.phase * Math.PI * 2);
    pb.gain.gain.setTargetAtTime((0.015 + fear * 0.09) * Math.max(0, ps) ** 2, t, 0.04);
    pb.filter.frequency.setTargetAtTime(ps > 0 ? 1300 : 900, t, 0.1);
    // Heartbeat: louder and faster with fear
    const hb = this.loops.heart;
    if (fear > 0.12 && t >= hb.next) {
      const bpm = 60 + fear * 90;
      hb.next = t + 60 / bpm;
      this.heartbeat(0.12 + fear * 0.55);
    }
```
REPLACE WITH:
```js
    // Player breath: speeds up with fear
    const pb = this.loops.pBreath;
    pb.phase += dt * (0.25 + fear * 0.9) * (1 - hide * 0.6);          // hidden: slow, held breath
    const ps = Math.sin(pb.phase * Math.PI * 2);
    pb.gain.gain.setTargetAtTime((0.015 + fear * 0.09) * (1 - hide * 0.7) * Math.max(0, ps) ** 2, t, 0.04);
    pb.filter.frequency.setTargetAtTime(ps > 0 ? 1300 : 900, t, 0.1);
    // Heartbeat: louder and faster with fear (and loud in your ears while hidden)
    const hb = this.loops.heart;
    if ((fear > 0.12 || hide > 0.5) && t >= hb.next) {
      const bpm = 60 + fear * 90 + hide * 20;
      hb.next = t + 60 / bpm;
      this.heartbeat(0.12 + fear * 0.55 + hide * 0.3);
    }
```

## PATCH #16 — 3. AUDIO ENGINE: Endless Descent layer — a throbbing sub and a cold high cluster that build per floor

INSERT AFTER:
```js
    [659, 698].forEach((f) => { const o = ctx.createOscillator(); o.frequency.value = f; const g = ctx.createGain(); g.gain.value = 0.02; o.connect(g); g.connect(m.tension); o.start(); });
    m.tensionOsc = ts;
    this.music = m;
```
NEW CODE:
```js
    // UPDATE 1: Endless Descent layer — a throbbing sub and a cold high cluster that build per floor
    m.descent = ctx.createGain(); m.descent.gain.value = 0; m.descent.connect(this.musicBus);
    const ds = ctx.createOscillator(); ds.type = 'sawtooth'; ds.frequency.value = 41.2;
    const dsf = ctx.createBiquadFilter(); dsf.type = 'lowpass'; dsf.frequency.value = 220; dsf.Q.value = 3;
    const dtrem = ctx.createGain(); dtrem.gain.value = 0.4;
    const dl = ctx.createOscillator(); dl.frequency.value = 1.2;
    const dlg = ctx.createGain(); dlg.gain.value = 0.35;
    dl.connect(dlg); dlg.connect(dtrem.gain); dl.start();
    ds.connect(dsf); dsf.connect(dtrem); dtrem.connect(m.descent); ds.start();
    [329.6, 349.2, 466.2].forEach((f) => { const o = ctx.createOscillator(); o.frequency.value = f; const g = ctx.createGain(); g.gain.value = 0.025; o.connect(g); g.connect(m.descent); o.start(); });
    m.descentLfo = dl; m.descentFilter = dsf;
```

## PATCH #17 — 3. AUDIO ENGINE: edit: updateMusic(dt, droneLvl, tension, chase, descent = 0) {

FIND:
```js
    }
  },
  updateMusic(dt, droneLvl, tension, chase) {
    if (!this.ready || !this.music) return;
    const m = this.music, t = this.now;
    m.drone.gain.setTargetAtTime(droneLvl * 0.16, t, 0.8);
```
REPLACE WITH:
```js
    }
  },
  updateMusic(dt, droneLvl, tension, chase, descent = 0) {
    if (!this.ready || !this.music) return;
    const m = this.music, t = this.now;
    m.descent.gain.setTargetAtTime(descent * 0.2, t, 1.2);
    if (descent > 0) { m.descentLfo.frequency.setTargetAtTime(1.2 + descent * 3.5, t, 1); m.descentFilter.frequency.setTargetAtTime(220 + descent * 500, t, 1); }
    m.drone.gain.setTargetAtTime(droneLvl * 0.16, t, 0.8);
```

## PATCH #18 — 3. AUDIO ENGINE: the Heart's walls

INSERT AFTER:
```js
    if (a.gusts && (T.wind -= dt) <= 0) { T.wind = 6 + Math.random() * 12; this.whoosh(around(20, 2, 8), 0.18 * a.gusts); }
    if (a.bells && (T.bird -= dt) <= 0) { T.bird = 20 + Math.random() * 30; this.chime(around(50, 5, 20), 0.12, 180 + Math.random() * 80); }
  },
```
NEW CODE:
```js
    if (a.wet && (T.wet -= dt) <= 0) { T.wet = (3 + Math.random() * 6) / a.wet; this.wetCreak(around(15, 0, 8), 0.3 + Math.random() * 0.3); }   // UPDATE 1: the Heart's walls
```

## PATCH #19 — 4. COLLISION WORLD: raycast that also reports the hit point and the surface normal (Crawlers walk on it).

INSERT AFTER:
```js
  },

  // Is the straight segment a→b blocked for a body of radius r? (samples spheres; used by Warden nav)
```
NEW CODE:
```js
  // UPDATE 1: raycast that also reports the hit point and the surface normal (Crawlers walk on it).
  // out = { t, collider, point: Vector3, normal: Vector3 }
  raycastHit(origin, dir, maxDist, filter, out) {
    if (!this.raycast(origin, dir, maxDist, filter, out)) return false;
    out.point.copy(origin).addScaledVector(dir, out.t);
    this.normalAt(out.collider, out.point, out.normal, dir);
    return true;
  },
  // Outward normal of a collider's surface nearest to point P (flipped to face against dir if given)
  normalAt(c, P, outN, dir) {
    if (c.type === 'plane') outN.copy(c.normal);
    else {
      const L = _w2.copy(P).sub(c.center).applyQuaternion(c.invQuat);
      if (c.type === 'box') {
        const h = c.half;
        const dx = Math.abs(Math.abs(L.x) - h.x), dy = Math.abs(Math.abs(L.y) - h.y), dz = Math.abs(Math.abs(L.z) - h.z);
        if (dx <= dy && dx <= dz) outN.set(Math.sign(L.x) || 1, 0, 0);
        else if (dy <= dz) outN.set(0, Math.sign(L.y) || 1, 0);
        else outN.set(0, 0, Math.sign(L.z) || 1);
      } else {
        const rxz = Math.sqrt(L.x * L.x + L.z * L.z);
        if (rxz < 1e-6 || Math.abs(Math.abs(L.y) - c.halfH) < Math.abs(rxz - c.radius)) outN.set(0, Math.sign(L.y) || 1, 0);
        else outN.set(L.x / rxz, 0, L.z / rxz);
      }
      outN.applyQuaternion(c.quat);
    }
    if (dir && outN.dot(dir) > 0) outN.negate();
    return outN;
  },

```

## PATCH #20 — 5. PLAYER & LOCOMOTION: a hand that holds a prop, grips a cord or carries a Crawler cannot anchor

FIND:
```js
    this.worldQuat = new THREE.Quaternion();
    this.contact = new Contact();
  }
  averageVelocity(out) {
```
REPLACE WITH:
```js
    this.worldQuat = new THREE.Quaternion();
    this.contact = new Contact();
    // UPDATE 1: a hand that holds a prop, grips a cord or carries a Crawler cannot anchor
    this.holding = null; this.cord = null; this.cling = null;
    this.gripWas = false; this.wet = false; this.touchSoundT = 0;
  }
  busy() { return !!(this.holding || this.cord || this.cling); }
  averageVelocity(out) {
```

## PATCH #21 — 5. PLAYER & LOCOMOTION: UPDATE 1

INSERT AFTER:
```js
  frameRigStart: new THREE.Vector3(),
  frozen: false,

```
NEW CODE:
```js
  groundCollider: null, landNoiseT: 0, inWater: false,   // UPDATE 1
```

## PATCH #22 — 5. PLAYER & LOCOMOTION: submerged = slippery

FIND:
```js
      if (!h.anchored) continue;
      if (!h.collider || !h.collider.enabled) { this.release(h, false); continue; }
      const surf = S[h.surface];
      _delta.copy(h.tracked).sub(h.anchor);
```
REPLACE WITH:
```js
      if (!h.anchored) continue;
      if (!h.collider || !h.collider.enabled) { this.release(h, false); continue; }
      const surf = Water.active && h.anchor.y < Water.level ? Water.surface(h.surface) : S[h.surface];   // UPDATE 1: submerged = slippery
      _delta.copy(h.tracked).sub(h.anchor);
```

## PATCH #23 — 5. PLAYER & LOCOMOTION: a submerged body sinks slowly and drags (you cannot swim: climb out)

FIND:
```js
    // --- 2. velocity integration
    const holding = drive && (this.hands[0].anchored || this.hands[1].anchored);
    if (!drive) this.desktopMove(dt);
    if (holding) {
      let grip = 0, cnt = 0;
      for (const h of this.hands) if (h.anchored) { grip += S[h.surface].bodyGrip; cnt++; }
      grip /= cnt;
      this.vel.y += CONFIG.GRAVITY * dt * (1 - grip);
      for (const h of this.hands) if (h.anchored) { const vn = this.vel.dot(h.normal); if (vn < 0) this.vel.addScaledVector(h.normal, -vn); }
```
REPLACE WITH:
```js
    // --- 2. velocity integration
    const holding = drive && (this.hands[0].anchored || this.hands[1].anchored);
    // UPDATE 1: a submerged body sinks slowly and drags (you cannot swim: climb out)
    this.inWater = Water.active && this.head.y + CONFIG.BODY_OFFSET_Y < Water.level;
    const gScale = this.inWater ? U1.WATER_GRAVITY : 1;
    if (!drive) this.desktopMove(dt);
    if (holding) {
      let grip = 0, cnt = 0;
      for (const h of this.hands) if (h.anchored) { grip += (Water.active && h.anchor.y < Water.level ? Water.surface(h.surface) : S[h.surface]).bodyGrip; cnt++; }
      grip /= cnt;
      this.vel.y += CONFIG.GRAVITY * dt * (1 - grip) * gScale;
      for (const h of this.hands) if (h.anchored) { const vn = this.vel.dot(h.normal); if (vn < 0) this.vel.addScaledVector(h.normal, -vn); }
```

## PATCH #24 — 5. PLAYER & LOCOMOTION: edit: if (!this.god) this.vel.y += CONFIG.GRAVITY * dt * gScale;

FIND:
```js
      this.supportY = this.head.y;
    } else {
      if (!this.god) this.vel.y += CONFIG.GRAVITY * dt;
      const sp = this.vel.length();
```
REPLACE WITH:
```js
      this.supportY = this.head.y;
    } else {
      if (!this.god) this.vel.y += CONFIG.GRAVITY * dt * gScale;
      const sp = this.vel.length();
```

## PATCH #25 — 5. PLAYER & LOCOMOTION: edit: if (this.inWater) this.vel.multiplyScalar(Math.exp(-U1.WATER_DRAG * dt…

INSERT AFTER:
```js
      this.moveRig(_move);
    }

```
NEW CODE:
```js
    if (this.inWater) this.vel.multiplyScalar(Math.exp(-U1.WATER_DRAG * dt));
```

## PATCH #26 — 5. PLAYER & LOCOMOTION: water slows a free hand — it follows the controller sluggishly

INSERT AFTER:
```js
    const R = CONFIG.HAND_RADIUS;
    _sweepFrom.copy(h.phys);
    const dist = _sweepFrom.distanceTo(h.tracked);
```
NEW CODE:
```js
    // UPDATE 1: water slows a free hand — it follows the controller sluggishly
    if (Water.active && h.phys.y < Water.level) h.tracked.lerpVectors(h.phys, h.tracked, Math.min(1, dt * 12 * U1.WATER_HAND_SLOW));
```

## PATCH #27 — 5. PLAYER & LOCOMOTION: a full hand still knocks against things

FIND:
```js
    if (hit) {
      h.touchTime = Game.time;
      if (h.cooldown <= 0) this.anchorHand(h, c);
    }
```
REPLACE WITH:
```js
    if (hit) {
      h.touchTime = Game.time;
      if (h.cooldown <= 0 && !h.busy()) this.anchorHand(h, c);
      else if (h.busy() && h.worldVel.dot(c.normal) < -0.3 && Game.time - h.touchSoundT > 0.25) {   // a full hand still knocks against things
        h.touchSoundT = Game.time;
        Game.onHandImpact(h, c.collider, -h.worldVel.dot(c.normal), h.phys, c.normal);
      }
    }
```

## PATCH #28 — 5. PLAYER & LOCOMOTION: a hard landing thumps (only Crawlers listen for it)

FIND:
```js
  onBodyContact(c) {
    const vn = this.vel.dot(c.normal);
    if (vn < 0) this.vel.addScaledVector(c.normal, -vn);
    if (c.normal.y > 0.55) { this.grounded = true; this.groundTime = Game.time; }
    else if (Math.abs(c.normal.y) < 0.6) { this.wallTime = Game.time; this.wallNormal.copy(c.normal); }
```
REPLACE WITH:
```js
  onBodyContact(c) {
    const vn = this.vel.dot(c.normal);
    // UPDATE 1: a hard landing thumps (only Crawlers listen for it)
    if (vn < -2.6 && Game.time - this.landNoiseT > 0.3) { this.landNoiseT = Game.time; Game.noise(c.point, -vn * 0.5, 'land'); }
    if (vn < 0) this.vel.addScaledVector(c.normal, -vn);
    if (c.normal.y > 0.55) { this.grounded = true; this.groundTime = Game.time; this.groundCollider = c.collider; }
    else if (Math.abs(c.normal.y) < 0.6) { this.wallTime = Game.time; this.wallNormal.copy(c.normal); }
```

## PATCH #29 — 5. PLAYER & LOCOMOTION: E now starts Endless, so god mode flies up with Space only

FIND:
```js
    if (_wish.lengthSq() > 1) _wish.normalize();
    const speed = I.key('ShiftLeft') || I.key('ShiftRight') ? CONFIG.DESK_SPRINT_SPEED : CONFIG.DESK_MOVE_SPEED;
    if (this.god) {
      this.vel.x = _wish.x * speed * 1.6; this.vel.z = _wish.z * speed * 1.6;
      this.vel.y = ((I.key('KeyE') || I.key('Space') ? 1 : 0) - (I.key('KeyQ') ? 1 : 0)) * speed * 1.4;
      return;
```
REPLACE WITH:
```js
    if (_wish.lengthSq() > 1) _wish.normalize();
    const speed = I.key('ShiftLeft') || I.key('ShiftRight') ? CONFIG.DESK_SPRINT_SPEED : CONFIG.DESK_MOVE_SPEED;
    if (this.god) {   // UPDATE 1: E now starts Endless, so god mode flies up with Space only
      this.vel.x = _wish.x * speed * 1.6; this.vel.z = _wish.z * speed * 1.6;
      this.vel.y = ((I.key('Space') ? 1 : 0) - (I.key('KeyQ') ? 1 : 0)) * speed * 1.4;
      return;
```

## PATCH #30 — 5. PLAYER & LOCOMOTION: wading is slow

FIND:
```js
    const onGround = Game.time - this.groundTime < 0.12;
    const k = onGround ? 14 : 2.5;
    this.vel.x = damp(this.vel.x, _wish.x * speed, k, dt);
    this.vel.z = damp(this.vel.z, _wish.z * speed, k, dt);
    if (I.consumeJump && onGround) this.vel.y = CONFIG.DESK_JUMP_SPEED;
```
REPLACE WITH:
```js
    const onGround = Game.time - this.groundTime < 0.12;
    const k = onGround ? 14 : 2.5;
    const wk = this.inWater ? 0.45 : 1;   // UPDATE 1: wading is slow
    this.vel.x = damp(this.vel.x, _wish.x * speed * wk, k, dt);
    this.vel.z = damp(this.vel.z, _wish.z * speed * wk, k, dt);
    if (I.consumeJump && onGround) this.vel.y = CONFIG.DESK_JUMP_SPEED;
```

## PATCH #31 — 6. INPUT: one-frame desktop "shake" (X)

INSERT AFTER:
```js
  mouseNDC: new THREE.Vector2(),
  desktopActive: false,

```
NEW CODE:
```js
  shakePulse: false,   // UPDATE 1: one-frame desktop "shake" (X)
```

## PATCH #32 — 6. INPUT: edit: if (!this.keys.has(e.code)) this.onKeyPress(e.code, e);

FIND:
```js
    window.addEventListener('keydown', (e) => {
      if (this.xr) return;
      if (!this.keys.has(e.code)) this.onKeyPress(e.code);
      this.keys.add(e.code);
      if (e.code === 'Space' || e.code === 'Tab') e.preventDefault();
    });
```
REPLACE WITH:
```js
    window.addEventListener('keydown', (e) => {
      if (this.xr) return;
      if (!this.keys.has(e.code)) this.onKeyPress(e.code, e);
      this.keys.add(e.code);
      if (e.code === 'Space' || e.code === 'Tab' || e.altKey) e.preventDefault();
    });
```

## PATCH #33 — 6. INPUT: keys: X shake, Alt+W water, 7-9 new levels, E Endless, K Crawler, U unlock all

FIND:
```js
  },
  key(code) { return this.keys.has(code); },
  onKeyPress(code) {
    if (code === 'Space') this.consumeJump = true;
    if (!this.desktopActive) return;
    if (code === 'KeyF') Flashlight.toggle();
    const lv = { Digit1: 0, Digit2: 1, Digit3: 2, Digit4: 3, Digit5: 4, Digit6: 5 }[code];
    if (lv !== undefined) Game.debugLoadLevel(lv);
```
REPLACE WITH:
```js
  },
  key(code) { return this.keys.has(code); },
  onKeyPress(code, e) {
    if (code === 'Space') this.consumeJump = true;
    if (!this.desktopActive) return;
    // UPDATE 1 keys: X shake, Alt+W water, 7-9 new levels, E Endless, K Crawler, U unlock all
    if (code === 'KeyX') this.shakePulse = true;
    if (code === 'KeyW' && e && e.altKey) { Water.debugRaise(); return; }
    if (code === 'KeyE') Game.startEndless(1);
    if (code === 'KeyK') Crawlers.debugSpawn();
    if (code === 'KeyU') Game.unlockAll();
    if (code === 'KeyF') Flashlight.toggle();
    const lv = { Digit1: 0, Digit2: 1, Digit3: 2, Digit4: 3, Digit5: 4, Digit6: 5, Digit7: 6, Digit8: 7, Digit9: 8 }[code];
    if (lv !== undefined) Game.debugLoadLevel(lv);
```

## PATCH #34 — 7. THE WARDEN: slam / peek / check / memory / sleep / dying / hollow variant

INSERT AFTER:
```js
  stomps: 0,
  _filterBlock: null,

```
NEW CODE:
```js
  // UPDATE 1: slam / peek / check / memory / sleep / dying / hollow variant
  variant: 'normal', chestGlow: null,
  slam: null, slamHands: [new THREE.Vector3(), new THREE.Vector3()],
  peeks: [], peek: null, peekBack: 'PATROL', peekCool: 4, _pose: { hip: 0, lean: 0, neck: 0, reach: 0 },
  checkSpot: null, checked: new Set(), searchRemain: 0, scriptFocus: null,
  memory: null, memoryIdx: -1,
  wake: 0, everWoke: false, sleepK: 0, sleepKT: 0, breathPhase: 0, breathRate: 1,
  fallAngle: 0, fallTarget: new THREE.Vector3(), lastSeenT: -99, armWet: [false, false],
```

## PATCH #35 — 7. THE WARDEN: the Hollow Warden's glowing chest cavity (Nightmare only)

INSERT AFTER:
```js
    scene.add(this.debugLabel);

    root.visible = false;
```
NEW CODE:
```js
    // UPDATE 1: the Hollow Warden's glowing chest cavity (Nightmare only)
    const cg = new THREE.Group(); cg.position.set(0, WC.SPINE * 0.55, 0.52); spineG.add(cg);
    const hole = new THREE.Mesh(new THREE.SphereGeometry(0.62, 12, 10), new THREE.MeshBasicMaterial({ color: 0x050000 }));
    hole.scale.set(1, 1.3, 0.35); cg.add(hole);
    this.chestGlowMat = new THREE.MeshBasicMaterial({ color: 0xff5020, transparent: true, opacity: 0.8, blending: THREE.AdditiveBlending, depthWrite: false });
    const glow = new THREE.Mesh(new THREE.SphereGeometry(0.42, 12, 10), this.chestGlowMat);
    glow.scale.set(1, 1.3, 0.5); glow.position.z = 0.08; cg.add(glow);
    cg.visible = false; cg.traverse((o) => { o.frustumCulled = false; });
    this.chestGlow = cg;

```

## PATCH #36 — 7. THE WARDEN: Nightmare / Endless multipliers, Time Trial switches it off

INSERT AFTER:
```js
      reachSpeed: WC.REACH_SPEED, lookUp: 0, sightRange: WC.VISION_RANGE, crawlZone: null, breath: 1,
    }, cfg);
    this.mode = this.cfg.mode;
```
NEW CODE:
```js
    this.applyModeTuning();   // UPDATE 1: Nightmare / Endless multipliers, Time Trial switches it off
```

## PATCH #37 — 7. THE WARDEN: edit: this.setupUpdate1(level);

INSERT AFTER:
```js
    this.climb = null;
    this.stomps = 0;
    this.debugLabel.visible = this.debug && this.active;
```
NEW CODE:
```js
    this.setupUpdate1(level);
```

## PATCH #38 — 7. THE WARDEN: edit: if (this.mode === 'sleep') this.snapSleepPose();

INSERT AFTER:
```js
      this.root.visible = true;
      this.setState(this.cfg.startState || 'PATROL');
    }
```
NEW CODE:
```js
      if (this.mode === 'sleep') this.snapSleepPose();
```

## PATCH #39 — 7. THE WARDEN: it is falling, or dead

INSERT AFTER:
```js
      return;
    }
    let best = null, bd = -1;
```
NEW CODE:
```js
    if (this.mode === 'dying') return;                               // UPDATE 1: it is falling, or dead
    if (this.cfg.mode === 'sleep') { this.backToSleep(); return; }   // UPDATE 1: back to its nest
```

## PATCH #40 — 7. THE WARDEN: edit: this.scriptFocus = null;

FIND:
```js
    this.state = s; this.stateT = 0; this.phase = '';
    this.reach.active = false;
    if (s === 'HUNT' && prev !== 'HUNT' && prev !== 'REACH') {
      AudioSys.roar(this.headPos, 1);
```
REPLACE WITH:
```js
    this.state = s; this.stateT = 0; this.phase = '';
    this.reach.active = false;
    this.scriptFocus = null;
    if (s === 'HUNT' && prev !== 'HUNT' && prev !== 'REACH' && prev !== 'SLAM') {
      AudioSys.roar(this.headPos, 1);
```

## PATCH #41 — 7. THE WARDEN: Crawlers drop off its back, subtitles, "never seen"

FIND:
```js
      this.jawT = 0.75;
      setTimeout(() => { this.jawT = 0.2; }, 2200);
    }
    if (s === 'INVESTIGATE') this.investigateT = 0;
    if (s === 'SEARCH') this.searchT = this.cfg.searchTime * (0.8 + Math.random() * 0.4);
  },

  // ------------------------------------------------------------ SENSES
  hear(pos, loudness) {
    if (!this.active || !this.cfg || this.mode === 'silhouette' || this.mode === 'climb' || this.mode === 'gateSlam') return;
    const d = _wa.copy(pos).sub(this.headPos).length();
    const perceived = loudness * this.cfg.hearing * 12 / (12 + d);
    if (perceived < WC.HEAR_THRESHOLD) return;
    if (this.mode === 'chase') return;
    if (this.state === 'HUNT' || this.state === 'REACH') {
      if (!this.seesPlayer) this.lastKnown.copy(pos);
      return;
    }
    this.lookTarget.copy(pos);
    this.noiseTarget.copy(pos);
    if (this.state !== 'INVESTIGATE' || perceived > 2.5 || this.phase === 'look') {
      this.setState('INVESTIGATE');
```
REPLACE WITH:
```js
      this.jawT = 0.75;
      setTimeout(() => { this.jawT = 0.2; }, 2200);
      this.onHuntStart();   // UPDATE 1: Crawlers drop off its back, subtitles, "never seen"
    }
    if (s === 'INVESTIGATE') this.investigateT = 0;
    if (s === 'SEARCH') {
      this.searchT = this.cfg.searchTime * (0.8 + Math.random() * 0.4);
      if (prev === 'HUNT' || prev === 'REACH' || prev === 'SLAM') this.checked.clear();   // UPDATE 1: fresh set of hiding spots to open
    }
  },

  // ------------------------------------------------------------ SENSES
  // UPDATE 1: returns true when the noise lured it into investigating (BAIT); feeds the Nest wake meter
  hear(pos, loudness) {
    if (!this.active || !this.cfg || this.mode === 'silhouette' || this.mode === 'climb' || this.mode === 'gateSlam' || this.mode === 'dying') return false;
    const d = _wa.copy(pos).sub(this.headPos).length();
    const perceived = loudness * this.cfg.hearing * 12 / (12 + d);
    if (this.mode === 'sleep') { this.addWake(perceived * U1.WAKE_PER_NOISE); return false; }
    if (perceived < WC.HEAR_THRESHOLD) return false;
    if (this.mode === 'chase') return false;
    if (this.state === 'HUNT' || this.state === 'REACH' || this.state === 'SLAM') {
      if (!this.seesPlayer) this.lastKnown.copy(pos);
      return false;
    }
    if ((this.state === 'CHECK' || this.state === 'PEEK') && perceived < 2.5) return false;   // busy, unless it is loud
    this.lookTarget.copy(pos);
    this.noiseTarget.copy(pos);
    if (this.state !== 'INVESTIGATE' || perceived > 2.5 || this.phase === 'look') {
      if (this.state === 'CHECK' && this.checkSpot) this.checkSpot.wardenRelease();
      this.setState('INVESTIGATE');
```

## PATCH #42 — 7. THE WARDEN: edit: return true;

FIND:
```js
      this.phase = 'go';
      if (Math.random() < 0.5) AudioSys.jointCreak(this.headPos);
    }
  },
```
REPLACE WITH:
```js
      this.phase = 'go';
      if (Math.random() < 0.5) AudioSys.jointCreak(this.headPos);
      return true;
    }
    return false;
  },
```

## PATCH #43 — 7. THE WARDEN: a narrow, close look through a gap

FIND:
```js
    const P = Player.head;
    this.seesPlayer = false;
    if (!this.cfg.canSee || Game.state !== 'PLAYING') { this.awareness = Math.max(0, this.awareness - 0.05); return; }
    const eye = this.headPos;
```
REPLACE WITH:
```js
    const P = Player.head;
    this.seesPlayer = false;
    if (!this.cfg.canSee || Game.state !== 'PLAYING' || this.mode === 'sleep' || this.mode === 'dying') { this.awareness = Math.max(0, this.awareness - 0.05); return; }
    const peeking = this.state === 'PEEK' && this.phase === 'hold';   // UPDATE 1: a narrow, close look through a gap
    const eye = this.headPos;
```

## PATCH #44 — 7. THE WARDEN: hidden in a locker/barrel/wardrobe: it can't see you, unless it is hunting and saw you cli

FIND:
```js
    let pointing = false;
    if (fl) { _wb.copy(eye).sub(Flashlight.light.position).normalize(); pointing = _wb.dot(Flashlight.beamDir) > Math.cos(0.5); }
    const range = this.cfg.sightRange * clamp(0.3 + light * 0.55, 0.3, 1.35) * (pointing ? 1.7 : 1);
    let visible = dist < range;
    if (visible && dist > 3.5) {
      const cosHalf = Math.cos(WC.VISION_FOV_DEG * DEG / 2);
      visible = _wb.copy(_wa).divideScalar(dist).dot(this.headFwd) > cosHalf;
```
REPLACE WITH:
```js
    let pointing = false;
    if (fl) { _wb.copy(eye).sub(Flashlight.light.position).normalize(); pointing = _wb.dot(Flashlight.beamDir) > Math.cos(0.5); }
    const range = (peeking ? U1.PEEK_RANGE : this.cfg.sightRange) * clamp(0.3 + light * 0.55, 0.3, 1.35) * (pointing ? 1.7 : 1);
    let visible = dist < range;
    // UPDATE 1: hidden in a locker/barrel/wardrobe: it can't see you, unless it is hunting and saw you climb in
    if (Hiding.current && !((this.state === 'HUNT' || this.state === 'REACH' || this.state === 'SLAM') && Hiding.seenEnter)) visible = false;
    if (visible && dist > 3.5) {
      const cosHalf = Math.cos((peeking ? U1.PEEK_FOV_DEG : WC.VISION_FOV_DEG) * DEG / 2);
      visible = _wb.copy(_wa).divideScalar(dist).dot(this.headFwd) > cosHalf;
```

## PATCH #45 — 7. THE WARDEN: edit: if (this.seesPlayer) { this.lastKnown.copy(P); this.lastSeenT = Game.t…

FIND:
```js
      this.awareness = Math.max(0, this.awareness - WC.SENSE_INTERVAL * 0.2);
    }
    if (this.seesPlayer) this.lastKnown.copy(P);
  },
```
REPLACE WITH:
```js
      this.awareness = Math.max(0, this.awareness - WC.SENSE_INTERVAL * 0.2);
    }
    if (this.seesPlayer) { this.lastKnown.copy(P); this.lastSeenT = Game.time; }
  },
```

## PATCH #46 — 7. THE WARDEN: else if (this.mode === 'dying') this.thinkDying(dt);     // UPDATE 1

INSERT AFTER:
```js
    if (this.senseT <= 0) { this.senseT = WC.SENSE_INTERVAL; this.sense(); }
    if (this.mode === 'silhouette') this.thinkSilhouette(dt);
    else if (this.mode === 'gateSlam') this.thinkGateSlam(dt);
```
NEW CODE:
```js
    else if (this.mode === 'sleep') this.thinkSleep(dt);     // UPDATE 1
    else if (this.mode === 'dying') this.thinkDying(dt);     // UPDATE 1
```

## PATCH #47 — 7. THE WARDEN: SLAM / PEEK / CHECK

FIND:
```js
    this.armMode[0] = this.armMode[1] = 'walk';
    this.postT.lean = 0.5; this.postT.hip = WC.HIP_HEIGHT; this.postT.neck = 0.5 - cfg.lookUp;
    if (this.awareness >= 1 && this.seesPlayer && this.state !== 'HUNT' && this.state !== 'REACH' && cfg.canSee) this.setState('HUNT');
    switch (this.state) {
```
REPLACE WITH:
```js
    this.armMode[0] = this.armMode[1] = 'walk';
    this.postT.lean = 0.5; this.postT.hip = WC.HIP_HEIGHT; this.postT.neck = 0.5 - cfg.lookUp;
    if (this.awareness >= 1 && this.seesPlayer && this.state !== 'HUNT' && this.state !== 'REACH' && this.state !== 'SLAM' && cfg.canSee) {
      if (this.state === 'CHECK' && this.checkSpot) this.checkSpot.wardenRelease();
      this.setState('HUNT');
    }
    if (this.thinkUpdate1(dt)) return;   // UPDATE 1: SLAM / PEEK / CHECK
    switch (this.state) {
```

## PATCH #48 — 7. THE WARDEN: it remembers where it last caught you

FIND:
```js
        if (this.arrived && list.length) {
          this.patrolIdx = (this.patrolIdx + 1) % list.length;
          const n = this.nav[list[this.patrolIdx]];
          if (n) this.goTo(n.p);
        }
        this.idleLook(dt);
        if (Math.random() < dt / 30) AudioSys.moan(this.headPos, 0.6);
```
REPLACE WITH:
```js
        if (this.arrived && list.length) {
          this.patrolIdx = (this.patrolIdx + 1) % list.length;
          let n = this.nav[list[this.patrolIdx]];
          // UPDATE 1: it remembers where it last caught you
          if (this.memoryIdx >= 0 && Math.random() < U1.MEMORY_PATROL_CHANCE) n = this.nav[this.memoryIdx];
          if (n) this.goTo(n.p);
        }
        this.idleLook(dt);
        if (this.maybePeek(dt, null)) break;   // UPDATE 1
        if (Math.random() < dt / 30) AudioSys.moan(this.headPos, 0.6);
```

## PATCH #49 — 7. THE WARDEN: out of reach on something it can smash

INSERT AFTER:
```js
        if (this.repathT <= 0) { this.repathT = 0.5; this.goTo(tgt); }
        this.lookTarget.copy(tgt);
        if (!this.seesPlayer) { this.lostT += dt; if (this.lostT > WC.LOSE_SIGHT_TIME) { this.setState('SEARCH'); break; } }
```
NEW CODE:
```js
        if (this.maybeSlam()) break;   // UPDATE 1: out of reach on something it can smash
```

## PATCH #50 — 7. THE WARDEN: open hiding spots near where it lost you, or put its eye to a nearby gap

INSERT AFTER:
```js
          }
          if (this.stateT > 5.5) {
            // next: a random nearby waypoint (a likely hiding place)
```
NEW CODE:
```js
            // UPDATE 1: open hiding spots near where it lost you, or put its eye to a nearby gap
            const spot = Hiding.spotToCheck(this.lastKnown, this.checked);
            if (spot) { this.startCheck(spot); break; }
            if (this.maybePeek(dt, this.lastKnown)) break;
```

## PATCH #51 — 7. THE WARDEN: it saw you climb in

INSERT AFTER:
```js
      case 'REACH': {
        this.lookTarget.copy(P);
        // shuffle closer while the arm is out, if we can
```
NEW CODE:
```js
        if (Hiding.current && Hiding.seenEnter) Hiding.forceOpen();   // UPDATE 1: it saw you climb in
```

## PATCH #52 — 7. THE WARDEN: it stands to peek in at windows

FIND:
```js
    this.speed = damp(this.speed, this.speedT, this.speedT > this.speed ? 1.8 : 3, dt);
    const crawlZone = this.cfg.crawlZone;
    if (crawlZone) {
      const z = crawlZone;
```
REPLACE WITH:
```js
    this.speed = damp(this.speed, this.speedT, this.speedT > this.speed ? 1.8 : 3, dt);
    const crawlZone = this.cfg.crawlZone;
    if (crawlZone && this.state !== 'PEEK') {   // UPDATE 1: it stands to peek in at windows
      const z = crawlZone;
```

## PATCH #53 — 7. THE WARDEN: collapsing

INSERT AFTER:
```js
    this.root.position.copy(this.pos);
    this.root.quaternion.setFromAxisAngle(UP, this.yaw);
  },
```
NEW CODE:
```js
    if (this.fallAngle > 0) this.root.quaternion.multiply(_wq.setFromAxisAngle(XAXIS, this.fallAngle));   // UPDATE 1: collapsing
```

## PATCH #54 — 7. THE WARDEN: sleepK blends toward lying face-down in its nest

FIND:
```js
    const crawlHip = 3.1, crawlLean = 1.42, crawlNeck = -1.05;
    const climbing = this.mode === 'climb' && this.climb && this.climb.phase !== 'rim';
    const hipT = climbing ? 0 : lerp(t.hip, crawlHip, p.crawl);
    const leanT = lerp(t.lean, crawlLean, p.crawl);
    const neckT = lerp(t.neck, crawlNeck, p.crawl);
    p.hip = damp(p.hip, hipT, climbing ? 8 : 2.2, dt);
```
REPLACE WITH:
```js
    const crawlHip = 3.1, crawlLean = 1.42, crawlNeck = -1.05;
    const climbing = this.mode === 'climb' && this.climb && this.climb.phase !== 'rim';
    // UPDATE 1: sleepK blends toward lying face-down in its nest
    this.sleepK = damp(this.sleepK, this.sleepKT, this.sleepKT > this.sleepK ? 1.5 : 0.9, dt);
    const sk = this.sleepK;
    const hipT = climbing ? 0 : lerp(lerp(t.hip, crawlHip, p.crawl), 1.5, sk);
    const leanT = lerp(lerp(t.lean, crawlLean, p.crawl), 1.5, sk);
    const neckT = lerp(lerp(t.neck, crawlNeck, p.crawl), -0.35, sk);
    p.hip = damp(p.hip, hipT, climbing ? 8 : 2.2, dt);
```

## PATCH #55 — 7. THE WARDEN: deep sleeping breaths that quicken as it stirs

FIND:
```js
    for (const l of this.legs) if (l.stepping) { bob += Math.sin(Math.PI * l.t) * 0.22; swayTarget += -l.side * 0.05; }
    this.bob = damp(this.bob, bob - 0.12 * Math.min(1, this.speed / 2), 8, dt);
    const breathe = Math.sin(this.time * 1.1) * 0.05;

```
REPLACE WITH:
```js
    for (const l of this.legs) if (l.stepping) { bob += Math.sin(Math.PI * l.t) * 0.22; swayTarget += -l.side * 0.05; }
    this.bob = damp(this.bob, bob - 0.12 * Math.min(1, this.speed / 2), 8, dt);
    this.breathPhase += dt * 1.1 * this.breathRate;
    const breathe = Math.sin(this.breathPhase) * (0.05 + 0.06 * sk);   // UPDATE 1: deep sleeping breaths that quicken as it stirs

```

## PATCH #56 — 7. THE WARDEN: the Hollow Warden's eyes and chest burn red

FIND:
```js
    // eyes brighten when hunting
    const hunting = this.state === 'HUNT' || this.state === 'REACH' || this.mode === 'chase';
    this.eyeMat.color.setHex(hunting ? 0xffe0a0 : 0x8f8068);

```
REPLACE WITH:
```js
    // eyes brighten when hunting
    const hunting = this.state === 'HUNT' || this.state === 'REACH' || this.mode === 'chase';
    if (this.variant === 'hollow') {   // UPDATE 1: the Hollow Warden's eyes and chest burn red
      this.eyeMat.color.setHex(hunting ? 0xff3020 : 0x902010);
      this.chestGlowMat.opacity = 0.55 + 0.35 * Math.sin(this.time * (hunting ? 7 : 2.2));
    } else if (this.mode === 'sleep') this.eyeMat.color.setRGB(0.12 + this.wake * 0.4, 0.1 + this.wake * 0.35, 0.08 + this.wake * 0.25);
    else this.eyeMat.color.setHex(hunting ? 0xffe0a0 : 0x8f8068);

```

## PATCH #57 — 7. THE WARDEN: wading

INSERT AFTER:
```js
    }
    Game.onWardenFootstep(l.planted, l.strength, false);
  },
```
NEW CODE:
```js
    if (Water.active && l.planted.y < Water.level) Water.splash(l.planted, l.strength);   // UPDATE 1: wading
  },
  // UPDATE 1: what a hand in reach/scripted/smash/slam mode turns its palm toward
  handFocus(mode, out) {
    if (mode === 'slam' && this.slam) return out.copy(this.slam.slamPoint || this.slam.center);
    if (mode === 'scripted' && this.scriptFocus) return out.copy(this.scriptFocus);
    if (mode === 'scripted' && this.gate) return out.set(this.gate.x, this.gate.y + 2.4, this.gate.z - 2);
    return out.copy(Player.head);
```

## PATCH #58 — 7. THE WARDEN: both hands driven by the slam

INSERT AFTER:
```js
        a.pos.copy(this.reach.active || mode === 'scripted' ? this.reach.hand : a.pos);
        this.fingerCurlT[i] = mode === 'scripted' ? this.fingerCurlT[i] : this.fingerCurlT[i];
      } else if (mode === 'smash') {
```
NEW CODE:
```js
      } else if (mode === 'slam') {   // UPDATE 1: both hands driven by the slam
        a.pos.copy(this.slamHands[i]);
```

## PATCH #59 — 7. THE WARDEN: wading — knuckles drag through the surface and splash

INSERT AFTER:
```js
        _wl.y = this.groundY + lerp(0.35, 1.8, drag) + swing * 0.5;
        if (this.state === 'HUNT' || this.mode === 'chase') _wl.y += 1.2;
        a.pos.lerp(_wl, 1 - Math.exp(-6 * dt));
```
NEW CODE:
```js
        if (Water.active) {   // UPDATE 1: wading — knuckles drag through the surface and splash
          _wl.y = Math.max(_wl.y, Water.level - 0.5 + swing * 0.8);
          const under = a.pos.y < Water.level;
          if (under !== this.armWet[i] && this.speed > 0.3) Water.splash(a.pos, 0.5);
          this.armWet[i] = under;
        }
```

## PATCH #60 — 7. THE WARDEN: edit: if (mode === 'reach' || mode === 'scripted' || mode === 'smash' || mod…

FIND:
```js
      // hand orientation: continue the forearm, blended toward the task direction
      _wc.copy(tmpEnd).sub(tmpMid).normalize();
      if (mode === 'reach' || mode === 'scripted' || mode === 'smash') {
        root.worldToLocal(_wd.copy(mode === 'scripted' && this.gate ? _wl.set(this.gate.x, this.gate.y + 2.4, this.gate.z - 2) : Player.head));
        _wd.sub(tmpEnd).normalize();
```
REPLACE WITH:
```js
      // hand orientation: continue the forearm, blended toward the task direction
      _wc.copy(tmpEnd).sub(tmpMid).normalize();
      if (mode === 'reach' || mode === 'scripted' || mode === 'smash' || mode === 'slam') {
        root.worldToLocal(_wd.copy(this.handFocus(mode, _wl)));
        _wd.sub(tmpEnd).normalize();
```

## PATCH #61 — NEW SECTION — 7. THE WARDEN: whole section: 7b. THE WARDEN — UPDATE 1 BEHAVIOURS

INSERT AFTER:
```js
    this.soundT.creak -= dt;
    if (this.soundT.creak <= 0) { this.soundT.creak = 4 + Math.random() * 7; AudioSys.jointCreak(this.headPos); }
  },
```
NEW CODE:
```js
  },
};

/* =====================================================================
   7b. THE WARDEN — UPDATE 1 BEHAVIOURS
       SLAM, PEEK, CHECK (hiding spots), memory, the Nest's sleep and
       wake meter, the Heart's dying collapse, the Hollow variant.
       Mixed into the Warden object so the original brain is untouched.
   ===================================================================== */
Object.assign(Warden, {
  // ------------------------------------------------------------ MODES & VARIANT
  applyModeTuning() {
    const c = this.cfg;
    if (Game.mode === 'timetrial') c.mode = 'none';
    if (Game.mode === 'nightmare') {
      const N = U1.NIGHTMARE;
      c.hearing *= N.hearing; c.sight *= N.sight; c.sightRange *= N.sightRange;
      c.walkSpeed *= N.speed; c.huntSpeed *= N.speed; c.reachSpeed *= N.reachSpeed; c.searchTime *= N.searchTime;
      if (c.chaseBase) { c.chaseBase *= N.speed; c.chaseMax *= N.speed; }
      if (c.climbSpeed) c.climbSpeed *= N.speed;
    }
    if (Game.mode === 'endless') {
      const f = Game.endless.floor;
      const k = Math.min(U1.ENDLESS_MAX_SPEED_MULT, 1 + U1.ENDLESS_SPEED_PER_FLOOR * f);
      c.walkSpeed *= k; c.huntSpeed *= k; c.reachSpeed *= Math.min(1.5, k);
      c.hearing *= 1 + U1.ENDLESS_HEARING_PER_FLOOR * f;
    }
    this.setVariant(Game.mode === 'nightmare' ? 'hollow' : 'normal');
  },
  // THE HOLLOW WARDEN: darker skin, no jaw, longer fingers, a glowing hole in its chest
  setVariant(v) {
    if (this.variant === v) return;
    this.variant = v;
    const hollow = v === 'hollow';
    this.skinMat.color.setHex(hollow ? 0x6a6470 : 0xffffff);
    this.parts.jawG.scale.setScalar(hollow ? 0.001 : 1);
    for (const a of this.arms) for (const ch of a.fingers) ch[0].scale.y = hollow ? 1.45 : 1;
    this.chestGlow.visible = hollow;
    if (Game.faceJaw) Game.faceJaw.visible = !hollow;
  },
  setupUpdate1(level) {
    this.wake = 0; this.everWoke = false; this.fallAngle = 0;
    this.sleepK = this.sleepKT = this.mode === 'sleep' ? 1 : 0;
    this.breathRate = 1; this.slam = null; this.peek = null; this.checkSpot = null; this.scriptFocus = null;
    this.checked.clear(); this.lastSeenT = -99; this.armWet[0] = this.armWet[1] = false; this.peekCool = 6;
    this.peeks = (level.peeks || []).map((d) => {
      const eye = new THREE.Vector3().fromArray(d.eye), look = new THREE.Vector3().fromArray(d.look);
      const pose = this.peekPose(eye.y - this.groundY);
      const dir = _wa.set(look.x - eye.x, 0, look.z - eye.z).normalize();
      const stand = new THREE.Vector3(eye.x - dir.x * pose.reach, this.groundY, eye.z - dir.z * pose.reach);
      return { eye, look, stand, cool: 0 };
    });
    // memory: the waypoint nearest to where it last caught you in this level
    this.memoryIdx = -1;
    const m = Game.progress.lastCatch && Game.progress.lastCatch[Game.levelIndex];
    if (m && this.nav.length) this.memoryIdx = this.nearestNode(_wa.fromArray(m), false);
  },
  onHuntStart() {
    Subtitles.add('[ROAR]', this.headPos);
    Game.onWardenHunt();
    if (this.cfg.shed || Game.mode === 'nightmare' || Game.mode === 'endless') Crawlers.shed(U1.CRAWLER_SHED_ON_HUNT, this);
  },
  thinkUpdate1(dt) {
    for (let i = 0; i < this.peeks.length; i++) this.peeks[i].cool -= dt;
    if (this.state === 'SLAM') { this.thinkSlam(dt); return true; }
    if (this.state === 'PEEK') { this.thinkPeek(dt); return true; }
    if (this.state === 'CHECK') { this.thinkCheck(dt); return true; }
    return false;
  },

  // ------------------------------------------------------------ SLAM
  // In HUNT, out of reach on a slammable platform: walk up, raise both fists, bring them down.
  maybeSlam() {
    if (!this.cfg.canCatch) return false;
    const plat = Game.playerSlamTarget();
    if (!plat || plat.collapsed || this.playerReachable()) return false;
    const top = plat.slamPoint || plat.center;
    if (!this.seesPlayer && this.lastKnown.distanceTo(top) > 5) return false;   // it has to know you are up there
    if (Math.hypot(top.x - this.pos.x, top.z - this.pos.z) > U1.SLAM_RANGE + 15) return false;
    this.setState('SLAM');
    this.slam = plat; this.phase = 'approach';
    this.goTo(this.approachPoint(top, this.pos) || top);
    this.slamHands[0].copy(this.arms[0].pos); this.slamHands[1].copy(this.arms[1].pos);
    return true;
  },
  thinkSlam(dt) {
    const c = this.slam.slamPoint || this.slam.center;
    this.lookTarget.copy(c);
    if (this.slam.collapsed && this.phase === 'approach') { this.setState('HUNT'); return; }
    if (this.phase === 'approach') {
      this.speedT = this.cfg.huntSpeed;
      this.postT.lean = 0.75; this.postT.hip = WC.HIP_HEIGHT - 0.3;
      const dh = Math.hypot(c.x - this.pos.x, c.z - this.pos.z);
      if (dh < U1.SLAM_RANGE * 0.6 || this.arrived || this.stateT > 8) {
        if (dh > U1.SLAM_RANGE) { this.lastKnown.copy(Player.head); this.setState('SEARCH'); return; }
        this.phase = 'raise'; this.stateT = 0; this.path.length = 0; this.arrived = true;
        AudioSys.roar(this.headPos, 0.8); this.jawT = 0.8;
      }
      return;
    }
    this.speedT = 0;
    this.faceToward(c, dt, 2);
    this.armMode[0] = this.armMode[1] = 'slam';
    const raise = this.phase === 'raise';
    for (let i = 0; i < 2; i++) {
      const side = i ? 1 : -1;
      if (raise) this.slamHands[i].lerp(this.root.localToWorld(_wl.set(side * 2.2, WC.HIP_HEIGHT + WC.SPINE + 3.5, 1.5)), 1 - Math.exp(-5 * dt));
      else if (this.phase === 'down') this.slamHands[i].lerp(_wl.set(c.x + side * 0.9, c.y + 0.3, c.z), clamp(this.stateT / U1.SLAM_DOWN_TIME, 0, 1));
      this.fingerCurlT[i] = raise ? 0.3 : 0.95;
    }
    this.postT.lean = raise ? 0.2 : 1.0; this.postT.hip = raise ? WC.HIP_HEIGHT + 0.3 : WC.HIP_HEIGHT - 1.2;
    if (raise && this.stateT > U1.SLAM_RAISE_TIME) { this.phase = 'down'; this.stateT = 0; }
    else if (this.phase === 'down' && this.stateT >= U1.SLAM_DOWN_TIME) { this.phase = 'recover'; this.stateT = 0; Game.onSlam(this.slam); }
    else if (this.phase === 'recover' && this.stateT > 1.3) { this.jawT = 0.2; this.lastKnown.copy(Player.head); this.setState(this.seesPlayer ? 'HUNT' : 'SEARCH'); }
  },

  // ------------------------------------------------------------ PEEK
  // Posture that puts the eye at height ye (above its ground). Returns { hip, lean, neck, reach }.
  peekPose(ye) {
    const L = clamp(lerp(1.45, 0.1, (ye - 3.7) / 7.3), 0.1, 1.45);
    const P = this._pose;
    P.lean = L; P.neck = 1.37 - L;
    P.hip = clamp(ye - 4 * Math.cos(L) - 0.88, 2.4, WC.HIP_HEIGHT + 0.3);
    P.reach = 4 * Math.sin(L) + 1.97;
    return P;
  },
  maybePeek(dt, near) {
    if (!this.peeks.length) return false;
    if (near) {   // SEARCH: a gap that looks in on where it lost you
      for (const pk of this.peeks) if (pk.cool <= 0 && pk.look.distanceTo(near) < U1.PEEK_RANGE) { this.startPeek(pk); return true; }
      return false;
    }
    this.peekCool -= dt;
    if (this.peekCool > 0) return false;
    this.peekCool = 4;
    for (const pk of this.peeks) {
      if (pk.cool > 0 || Math.hypot(pk.stand.x - this.pos.x, pk.stand.z - this.pos.z) > 30) continue;
      if (Math.random() < U1.PEEK_CHANCE) { this.startPeek(pk); return true; }
    }
    return false;
  },
  startPeek(pk) {
    const back = this.state === 'SEARCH' ? 'SEARCH' : 'PATROL';
    this.searchRemain = this.searchT;
    this.setState('PEEK');
    this.peek = pk; this.peekBack = back; pk.cool = U1.PEEK_COOLDOWN;
    this.phase = 'go';
    this.goTo(pk.stand);
  },
  thinkPeek(dt) {
    const pk = this.peek;
    if (this.phase === 'go') {
      this.speedT = this.cfg.walkSpeed * 1.2;
      this.lookTarget.copy(pk.eye);
      if (this.arrived || this.nearGoal(1.5) || this.stateT > 20) { this.phase = 'in'; this.stateT = 0; AudioSys.sniff(this.headPos); }
      return;
    }
    this.speedT = 0; this.path.length = 0;
    this.faceToward(pk.look, dt, 1.0);
    if (this.phase === 'out') { if (this.stateT > 1.6) this.endPeek(); return; }
    const pose = this.peekPose(pk.eye.y - this.groundY);
    this.postT.hip = pose.hip; this.postT.lean = pose.lean; this.postT.neck = pose.neck; this.postT.crawl = 0;
    // shuffle so the eye lines up with the gap
    _wa.set(pk.eye.x - this.headPos.x, 0, pk.eye.z - this.headPos.z);
    const err = _wa.length();
    if (err > 0.25) this.pos.addScaledVector(_wa, Math.min(1, dt * 1.2));
    if (this.phase === 'in') {
      this.lookTarget.copy(pk.look);
      if (this.stateT > 3 || (err < 0.8 && Math.abs(this.headPos.y - pk.eye.y) < 0.8)) {
        this.phase = 'hold'; this.stateT = 0; this.jawT = 0.3;
        Subtitles.add('[slow breathing at the gap]', pk.eye);
      }
    } else {   // hold: the long look
      const a = this.stateT * 0.7;
      this.lookTarget.set(pk.look.x + Math.sin(a) * 2.5, pk.look.y + Math.sin(a * 1.7), pk.look.z + Math.cos(a) * 2.5);
      if (this.stateT > U1.PEEK_TIME) { this.phase = 'out'; this.stateT = 0; this.jawT = 0.15; }
    }
  },
  endPeek() {
    const back = this.peekBack, r = this.searchRemain;
    this.peek = null;
    this.setState(back);
    if (back === 'SEARCH') { this.searchT = r; this.phase = 'look'; } else this.arrived = true;
  },

  // ------------------------------------------------------------ CHECK (hiding spots)
  startCheck(spot) {
    this.searchRemain = this.searchT;
    this.setState('CHECK');
    this.checkSpot = spot; this.checked.add(spot);
    this.phase = 'go';
    this.goTo(this.approachPoint(spot.front, this.pos) || spot.front);
  },
  thinkCheck(dt) {
    const s = this.checkSpot;
    this.lookTarget.copy(s.center);
    if (this.phase === 'go') {
      this.speedT = this.cfg.walkSpeed * 1.3;
      if (this.arrived || this.nearGoal(2.5) || this.stateT > 15) { this.phase = 'open'; this.stateT = 0; AudioSys.sniff(this.headPos); }
      return;
    }
    this.speedT = 0; this.path.length = 0;
    this.faceToward(s.center, dt, 1.5);
    const low = s.center.y - this.groundY < 5;
    this.postT.hip = low ? 3.4 : WC.HIP_HEIGHT; this.postT.lean = low ? 1.1 : 0.4; this.postT.neck = low ? 0.15 : 0.4;
    const side = this.sideToward(s.handle);
    this.armMode[side < 0 ? 0 : 1] = 'scripted';
    this.scriptFocus = s.center;
    this.reach.active = true; this.reach.side = side;
    this.reach.hand.lerp(s.handle, 1 - Math.exp(-3 * dt));
    this.fingerCurlT[side < 0 ? 0 : 1] = 0.7;
    if (this.phase === 'open') {
      s.wardenOpen(clamp(this.stateT / U1.HIDE_CHECK_TIME, 0, 1));   // slowly, creaking
      if (this.stateT >= U1.HIDE_CHECK_TIME) {
        this.phase = 'look'; this.stateT = 0;
        if (Hiding.current === s && !Player.god && Game.state === 'PLAYING') { this.state = 'GRAB'; Game.caught(); return; }   // found you
        AudioSys.sniff(this.headPos);
      }
    } else if (this.stateT > 1.6) {
      s.wardenRelease();
      const r = this.searchRemain;
      this.setState('SEARCH');
      this.searchT = r; this.phase = 'look';
    }
  },

  // ------------------------------------------------------------ THE NEST: asleep
  snapSleepPose() {
    this.sleepK = this.sleepKT = 1;
    this.post.crawl = this.postT.crawl = 1;
    this.post.hip = 1.5; this.post.lean = 1.5; this.post.neck = -0.35;
    this.speed = this.speedT = 0;
  },
  backToSleep() {
    const st = this.cfg.start || [0, 0, 0];
    this.mode = 'sleep';
    this.teleport(_wa.set(st[0], this.groundY, st[2]), this.cfg.startYaw || 0);
    this.state = 'SLEEP'; this.stateT = 0; this.phase = '';
    this.wake = 0.35; this.awareness = 0; this.seesPlayer = false;
    this.snapSleepPose();
  },
  addWake(v) {
    if (this.mode !== 'sleep' || Game.state !== 'PLAYING') return;
    this.wake = Math.min(1, this.wake + v);
  },
  thinkSleep(dt) {
    this.speedT = 0; this.path.length = 0; this.arrived = true;
    this.armMode[0] = this.armMode[1] = 'walk';
    this.postT.crawl = 1;
    this.lookTarget.set(this.pos.x + Math.sin(this.yaw) * 10, this.groundY, this.pos.z + Math.cos(this.yaw) * 10);
    if (Game.state === 'PLAYING') {
      const dHead = Player.head.distanceTo(this.headPos);
      if (dHead < U1.WAKE_NEAR_RADIUS) this.addWake(U1.WAKE_NEAR_PER_SEC * dt * (1 + 2 * (1 - dHead / U1.WAKE_NEAR_RADIUS)));
      if (Flashlight.on && Flashlight.light.intensity > 1 && dHead < 15) {   // a light in its face
        _wb.copy(this.headPos).sub(Flashlight.light.position).normalize();
        if (_wb.dot(Flashlight.beamDir) > Math.cos(0.35)) this.addWake(U1.WAKE_LIGHT_PER_SEC * dt);
      }
    }
    this.wake = Math.max(0, this.wake - U1.WAKE_DECAY * dt);
    // the wake meter is its breathing: faster and louder as it surfaces
    this.breathRate = 0.55 + this.wake * 2.6;
    this.breathVol = this.cfg.breath * (0.7 + this.wake * 0.8);
    this.jawT = 0.05 + this.wake * 0.25;
    if (this.wake > 0.5 && Math.random() < dt * this.wake * 0.6) {
      this.postT.roll = (Math.random() - 0.5) * 0.3;
      if (Math.random() < 0.25) { AudioSys.moan(this.headPos, 0.35); Subtitles.add('[it groans in its sleep]', this.headPos); }
    }
    if (this.wake >= 1) this.wakeUp();
  },
  wakeUp() {
    this.mode = 'normal'; this.everWoke = true; this.sleepKT = 0; this.postT.crawl = 0;
    this.breathRate = 1; this.breathVol = this.cfg.breath;
    this.awareness = 1.2; this.lastKnown.copy(Player.head); this.lastSeenT = Game.time;
    this.setState('HUNT');
    Game.toast('IT IS AWAKE');
  },

  // ------------------------------------------------------------ THE HEART: hurt and dying
  hurt() {   // a cord snapped
    if (!this.active || this.mode === 'dying') return;
    AudioSys.roar(this.headPos, 1); this.jawT = 0.9; this.postT.roll = 0.35;
    Subtitles.add('[a scream of pain]', this.headPos);
    if (this.mode === 'normal' && this.state !== 'HUNT' && this.state !== 'REACH') { this.lastKnown.copy(Player.head); this.awareness = 1.1; this.setState('HUNT'); }
  },
  startDying(fallToward) {
    if (!this.active) return false;
    if (this.state === 'CHECK' && this.checkSpot) this.checkSpot.wardenRelease();
    this.mode = 'dying'; this.state = 'DYING'; this.phase = 'stagger'; this.stateT = 0;
    this.reach.active = false; this.slam = null; this.sleepKT = 0;
    this.fallTarget.copy(fallToward);
    // stagger toward a spot from where its body falls across the target
    _wa.set(this.fallTarget.x - this.pos.x, 0, this.fallTarget.z - this.pos.z);
    const d = _wa.length();
    if (d > 9.5) this.goTo(_wb.copy(this.fallTarget).addScaledVector(_wa.normalize(), -9));
    else { this.path.length = 0; this.arrived = true; }
    AudioSys.dyingMoan(this.headPos, 1);
    Subtitles.add('[a long, dying moan]', this.headPos);
    this.jawT = 0.85;
    return true;
  },
  thinkDying(dt) {
    this.armMode[0] = this.armMode[1] = 'walk';
    if (this.phase === 'stagger') {
      this.speedT = 1.1;
      this.postT.lean = 0.9 + Math.sin(this.stateT * 2.3) * 0.25; this.postT.hip = WC.HIP_HEIGHT - 0.8; this.postT.roll = Math.sin(this.stateT * 1.7) * 0.2;
      this.lookTarget.set(this.pos.x + Math.sin(this.yaw) * 6, this.groundY + 16, this.pos.z + Math.cos(this.yaw) * 6);
      if (this.stateT > 5 || this.arrived) { this.phase = 'fall'; this.stateT = 0; this.path.length = 0; }
    } else if (this.phase === 'fall') {
      this.speedT = 0;
      this.faceToward(this.fallTarget, dt, 0.5);
      const k = clamp(this.stateT / 5, 0, 1);          // slow motion: an accelerating 5 s topple
      this.fallAngle = 1.45 * k * k;
      this.postT.hip = lerp(WC.HIP_HEIGHT - 0.8, 3.2, k); this.postT.lean = 0.6;
      this.breathVol = this.cfg.breath * (1 - k);
      this.lookTarget.set(this.pos.x + Math.sin(this.yaw) * 10, this.groundY, this.pos.z + Math.cos(this.yaw) * 10);
      if (k >= 1) {
        this.phase = 'dead'; this.stateT = 0;
        AudioSys.crash(this.headPos, 1); AudioSys.thud(this.headPos, 2.5);
        Input.hapticBoth(1, 600);
        Dust.emit(this.headPos, 60, 8, 0x5a3030, -0.3, 3, 1.5);
        Game.onWardenFallen();
      }
    } else {
      this.speedT = 0; this.breathVol = 0; this.jawT = 0.5;
    }
  },
});

/* =====================================================================
   7c. CRAWLERS (UPDATE 1) — pale, eyeless, dog-sized things the Warden
       sheds from its back. Blind: they hunt by sound. They walk on
       walls and ceilings, squeeze into vents, and latch onto hands.
       All Crawlers share 5 instanced meshes (body, head, jaws, legs, blob).
   ===================================================================== */
const _ca = new THREE.Vector3(), _cb = new THREE.Vector3(), _cc = new THREE.Vector3(), _cd = new THREE.Vector3(), _ce = new THREE.Vector3();
const _cq = new THREE.Quaternion(), _cq2 = new THREE.Quaternion(), _cm = new THREE.Matrix4(), _cs = new THREE.Vector3(), _cr = new THREE.Euler();
const _cHit = { t: 0, collider: null, point: new THREE.Vector3(), normal: new THREE.Vector3() };
const ONE3 = new THREE.Vector3(1, 1, 1);
const JAW_FLIP = new THREE.Quaternion().setFromAxisAngle(ZAXIS, Math.PI);
// hip offsets in body space (x side, y up, z forward): L1 L2 L3 R1 R2 R3
const CRAWLER_HIPS = [[-0.09, 0, 0.12], [-0.11, 0, 0], [-0.09, 0, -0.13], [0.09, 0, 0.12], [0.11, 0, 0], [0.09, 0, -0.13]];
const CRAWLER_TRIPOD = [0, 1, 0, 1, 0, 1];   // tripod A = L1 R2 L3, tripod B = R1 L2 R3

class Crawler {
  constructor() {
    this.pos = new THREE.Vector3(); this.up = new THREE.Vector3(0, 1, 0); this.fwd = new THREE.Vector3(0, 0, 1);
    this.home = new THREE.Vector3(); this.homeUp = new THREE.Vector3(0, 1, 0);
    this.vel = new THREE.Vector3(); this.airborne = false;
    this.state = 'IDLE'; this.stateT = 0; this.shed = false;
    this.target = new THREE.Vector3(); this.fleeFrom = new THREE.Vector3(); this.wanderDir = new THREE.Vector3(1, 0, 0);
    this.heardT = -99; this.heardPlayer = false; this.wanderT = 0; this.pause = false;
    this.feet = [];
    for (let i = 0; i < 6; i++) this.feet.push({ pos: new THREE.Vector3(), from: new THREE.Vector3(), to: new THREE.Vector3(), t: 1, stepping: false });
    this.tri = [0, 0];
    this.gaitT = 0; this.bob = 0; this.jaw = 0.1; this.jawT = 0.1; this.speed = 0;
    this.jitter = new THREE.Vector3(); this.headJ = new THREE.Vector3(); this.jitterT = 0;
    this.hand = null; this.shakes = 0; this.shakeArmed = true; this.lastShakeT = -99; this.shriekT = 0; this.litT = 0;
    this.stuckT = 0; this.bestD = 1e9; this.chitterT = 3;
    this.quat = new THREE.Quaternion(); this.bodyPos = new THREE.Vector3();
    this.headPos = new THREE.Vector3(); this.headQuat = new THREE.Quaternion();
  }
}

const Crawlers = {
  list: [], pool: [], meshes: null, built: false, lit: 0, flashT: 0, near: [null, null, null], subT: 0,
  _filter: (c) => !c.noCrawl,

  build(scene) {
    const N = U1.CRAWLER_MAX;
    const mat = new THREE.MeshLambertMaterial({ map: getTexture('skin'), vertexColors: true });
    mat.color.setHex(0xb8b0a8);   // the Warden's skin, a shade darker
    mat.userData.shared = true;
    const pale = 0xe8e2d8, dark = 0x3a0c0c;
    // body: a hunched thorax and abdomen with spine knobs
    const bp = [];
    const thorax = colorizeGeometry(new THREE.SphereGeometry(0.11, 10, 8), pale); thorax.scale(1.1, 0.75, 1.35); thorax.translate(0, 0.02, 0.06); bp.push(thorax);
    const abdomen = colorizeGeometry(new THREE.SphereGeometry(0.12, 10, 8), pale); abdomen.scale(1.0, 0.85, 1.5); abdomen.translate(0, 0.05, -0.15); bp.push(abdomen);
    for (let k = 0; k < 6; k++) { const b = colorizeGeometry(new THREE.SphereGeometry(0.02, 5, 4), 0xc8c0b4); b.translate(0, 0.1 + Math.sin(k / 5 * Math.PI) * 0.035, 0.12 - k * 0.06); bp.push(b); }
    const bodyGeo = mergeGeometries(bp); bp.forEach((g) => g.dispose());
    // head: a long eyeless skull; the dark gullet shows when the jaws split open
    const hp = [];
    const skull = colorizeGeometry(new THREE.SphereGeometry(0.06, 10, 8), pale); skull.scale(1, 0.95, 1.9); skull.translate(0, 0.01, 0.05); hp.push(skull);
    const gullet = colorizeGeometry(new THREE.SphereGeometry(0.04, 8, 6), dark, 0.05); gullet.scale(0.7, 1.5, 1.6); gullet.translate(0, -0.005, 0.13); hp.push(gullet);
    const headGeo = mergeGeometries(hp); hp.forEach((g) => g.dispose());
    // one jaw half (two per Crawler, rotated apart): the mouth splits vertically
    const jp = [];
    const plate = colorizeGeometry(new THREE.SphereGeometry(0.035, 8, 6), pale); plate.scale(0.7, 1.35, 2.4); plate.translate(0, 0, 0.07); jp.push(plate);
    for (let k = 0; k < 4; k++) { const tooth = colorizeGeometry(new THREE.ConeGeometry(0.006, 0.025, 4), 0xd8d0b0); tooth.rotateZ(-Math.PI / 2); tooth.translate(0.022, -0.03 + k * 0.02, 0.12); jp.push(tooth); }
    const jawGeo = mergeGeometries(jp); jp.forEach((g) => g.dispose());
    // leg segment: unit length hanging along -Y, thick at the joint
    const legGeo = colorizeGeometry(new THREE.CylinderGeometry(1, 0.45, 1, 5, 1), 0xd8d0c4); legGeo.translate(0, -0.5, 0);
    // arachnophobia mode: a soft glowing blob
    const blobMat = new THREE.MeshBasicMaterial({ color: 0x9affd8, transparent: true, opacity: 0.8, depthWrite: false });
    blobMat.userData.shared = true;
    const mk = (geo, m, count) => {
      const im = new THREE.InstancedMesh(geo, m, count);
      im.count = 0; im.frustumCulled = false; im.instanceMatrix.setUsage(THREE.DynamicDrawUsage);
      scene.add(im); return im;
    };
    this.meshes = { body: mk(bodyGeo, mat, N), head: mk(headGeo, mat, N), jaw: mk(jawGeo, mat, N * 2), leg: mk(legGeo, mat, N * 12), blob: mk(new THREE.SphereGeometry(0.15, 14, 10), blobMat, N) };
    for (let i = 0; i < N; i++) this.pool.push(new Crawler());
    this.built = true;
  },

  // ------------------------------------------------------------ lifecycle
  clear() {
    for (const c of this.list) { this.detach(c); this.pool.push(c); }
    this.list.length = 0;
    this.render();
    for (let i = 0; i < 3; i++) AudioSys.setSkitter(i, 0, null);
  },
  setupLevel(data) {
    this.clear();
    const defs = data.crawlers || [];
    for (const d of defs) this.spawn(_ce.fromArray(d.p), d.n ? _cd.fromArray(d.n) : UP, 'IDLE');
  },
  spawn(p, n, state) {
    if (!this.built || this.list.length >= U1.CRAWLER_MAX) return null;
    const c = this.pool.pop();
    if (!c) return null;
    c.pos.copy(p); c.up.copy(n).normalize();
    c.fwd.set(Math.random() - 0.5, Math.random() - 0.5, Math.random() - 0.5);
    this.tangent(c, c.fwd);
    c.state = state || 'IDLE'; c.stateT = 0; c.airborne = false; c.vel.set(0, 0, 0); c.shed = false;
    c.hand = null; c.shakes = 0; c.heardT = -99; c.heardPlayer = false; c.jaw = c.jawT = 0.1; c.litT = 0; c.stuckT = 0; c.bestD = 1e9;
    c.chitterT = 2 + Math.random() * 5; c.wanderT = Math.random() * 2;
    this.snap(c);
    c.home.copy(c.pos); c.homeUp.copy(c.up);
    this.resetFeet(c);
    this.list.push(c);
    return c;
  },
  remove(c) {
    const i = this.list.indexOf(c);
    if (i < 0) return;
    this.detach(c);
    this.list.splice(i, 1);
    this.pool.push(c);
  },
  detach(c) { if (c.hand) { c.hand.cling = null; c.hand = null; } },
  // fwd made tangent to the surface (falls back to any tangent)
  tangent(c, v) {
    v.addScaledVector(c.up, -v.dot(c.up));
    if (v.lengthSq() < 1e-6) v.set(1, 0, 0).addScaledVector(c.up, -c.up.x);
    if (v.lengthSq() < 1e-6) v.set(0, 0, 1);
    return v.normalize();
  },
  // stick to the nearest surface along -up (or fall)
  snap(c) {
    _cb.copy(c.pos).addScaledVector(c.up, 0.4);
    _cc.copy(c.up).negate();
    if (World.raycastHit(_cb, _cc, 1.6, this._filter, _cHit)) {
      c.up.copy(_cHit.normal); c.pos.copy(_cHit.point).addScaledVector(c.up, U1.CRAWLER_BODY_HEIGHT);
      this.tangent(c, c.fwd); c.airborne = false;
    } else { c.airborne = true; c.vel.set(0, 0, 0); }
  },
  resetFeet(c) {
    this.frame(c);
    for (let i = 0; i < 6; i++) { this.footIdeal(c, i, 0, c.feet[i].pos); c.feet[i].stepping = false; c.feet[i].t = 1; }
    c.tri[0] = c.tri[1] = 0;
  },
  resetForRespawn() {
    for (let i = this.list.length - 1; i >= 0; i--) {
      const c = this.list[i];
      if (c.shed) { this.remove(c); continue; }
      this.detach(c);
      c.pos.copy(c.home); c.up.copy(c.homeUp); this.tangent(c, c.fwd);
      c.state = 'IDLE'; c.stateT = 0; c.airborne = false; c.vel.set(0, 0, 0); c.heardT = -99; c.jawT = 0.1;
      this.resetFeet(c);
    }
  },
  // the Warden sheds them from its back when a hunt begins
  shed(n, warden) {
    for (let k = 0; k < n; k++) {
      warden.parts.spineG.getWorldPosition(_ce); _ce.y += 2;
      const c = this.spawn(_ce, UP, 'STALK');
      if (!c) return;
      c.shed = true; c.airborne = true;
      c.vel.set((Math.random() - 0.5) * 5, 2 + Math.random() * 2, (Math.random() - 0.5) * 5);
      c.target.copy(Player.head); c.heardT = Game.time; c.heardPlayer = true;
      AudioSys.chitter(c.pos, 0.6);
    }
    Subtitles.add('[something drops off its back]', warden.headPos);
  },
  debugSpawn() {
    _ca.set(0, 0, -1).applyQuaternion(Player.headWorldQuat); _ca.y = 0; _ca.normalize();
    const c = this.spawn(_ce.copy(Player.head).addScaledVector(_ca, 3).setY(Player.head.y + 0.5), UP, 'IDLE');
    Game.toast(c ? 'CRAWLER SPAWNED' : 'CRAWLER LIMIT REACHED');
  },

  // ------------------------------------------------------------ senses
  // Blind: every noise in the game comes through here (shorter range than the Warden).
  hear(pos, loud, src) {
    if (src === 'crawler' || !this.list.length) return;
    const fromPlayer = pos.distanceTo(Player.head) < 2.5;
    for (const c of this.list) {
      if (c.state === 'CLING' || c.state === 'STUN' || c.state === 'FLEE' || c.state === 'FLINCH' || c.state === 'LUNGE' || c.airborne) continue;
      const d = c.pos.distanceTo(pos);
      const perceived = loud * Math.max(0, 1 - d / U1.CRAWLER_HEAR_RANGE);
      if (perceived < U1.CRAWLER_HEAR_THRESHOLD) continue;
      if (Grab.nearestLitFlare(pos, U1.FLARE_REPEL_RADIUS)) continue;   // never toward a burning flare
      c.target.copy(pos); c.heardT = Game.time; c.heardPlayer = fromPlayer; c.bestD = 1e9;
      if (c.state === 'IDLE') this.setState(c, 'LISTEN');
      else if (c.state === 'LISTEN') c.stateT = Math.min(c.stateT, U1.CRAWLER_LISTEN_TIME * 0.5);
      if (perceived > 2 && d < U1.CRAWLER_LUNGE_RANGE && fromPlayer) this.lunge(c, pos);   // right beside it: leaps at once
    }
  },
  setState(c, s, from) {
    c.state = s; c.stateT = 0;
    if (from) c.fleeFrom.copy(from);
    if (s === 'LISTEN') { c.jawT = 0.4; if (Math.random() < 0.6) AudioSys.chitter(c.pos, 0.5); }
    else if (s === 'IDLE') { c.jawT = 0.1; c.wanderT = 0; }
    else if (s === 'STALK') { c.stuckT = 0; c.bestD = 1e9; c.jawT = 0.2; }
    else if (s === 'FLEE' || s === 'FLINCH') c.jawT = 0.6;
  },

  // ------------------------------------------------------------ brain
  update(dt) {
    if (!this.list.length) { for (let i = 0; i < 3; i++) AudioSys.setSkitter(i, 0, null); return; }
    const playing = Game.state === 'PLAYING' || Game.state === 'MENU';
    if (playing) {
      for (let i = this.list.length - 1; i >= 0; i--) this.think(this.list[i], dt);
      this.flashCheck(dt);
    }
    this.render();
    this.sounds(dt, playing);
  },
  think(c, dt) {
    c.stateT += dt;
    if (c.state === 'CLING') { this.updateCling(c, dt); return; }
    if (c.airborne) { this.fly(c, dt); this.animate(c, dt, 0); return; }
    // they will not go in the water
    if (Water.active && c.pos.y < Water.level - 0.1) { Dust.emit(c.pos, 6, 0.2, 0xc8d8d8, 0.6, 1, 0.3); this.remove(c); return; }
    // a burning flare keeps them away
    const fl = Grab.litFlare;
    if (fl && c.state !== 'FLEE' && c.state !== 'STUN' && fl.pos.distanceTo(c.pos) < U1.FLARE_REPEL_RADIUS) this.setState(c, 'FLEE', fl.pos);
    let speed = 0;
    const dir = _cd;
    switch (c.state) {
      case 'IDLE': {   // clinging, twitching, creeping about near home
        c.wanderT -= dt;
        if (c.wanderT <= 0) {
          c.wanderT = 1.5 + Math.random() * 3;
          c.pause = Math.random() < 0.45;
          if (c.pos.distanceTo(c.home) > 4) c.wanderDir.copy(c.home).sub(c.pos);
          else c.wanderDir.set(Math.random() - 0.5, Math.random() - 0.5, Math.random() - 0.5);
        }
        if (!c.pause) speed = U1.CRAWLER_SPEED_IDLE;
        dir.copy(c.wanderDir);
        break;
      }
      case 'LISTEN': {   // freezes, head toward the sound
        dir.copy(c.target).sub(c.pos);
        this.turnToward(c, dir, dt);
        if (c.stateT > U1.CRAWLER_LISTEN_TIME) this.setState(c, 'STALK');
        break;
      }
      case 'STALK': {
        speed = U1.CRAWLER_SPEED_STALK;
        dir.copy(c.target).sub(c.pos);
        const d = dir.length();
        if (c.heardPlayer && Game.time - c.heardT < 2.5 && d < U1.CRAWLER_LUNGE_RANGE && Game.state === 'PLAYING') { this.lunge(c, c.target); return; }
        // on a ceiling right above the sound: let go and drop
        if (c.up.y < -0.5 && Math.hypot(c.target.x - c.pos.x, c.target.z - c.pos.z) < 1.5 && c.pos.y - c.target.y > 1) { c.airborne = true; c.vel.set(0, -0.5, 0); return; }
        if (d < 0.7) { speed = 0; if (Game.time - c.heardT > 2) { c.home.copy(c.pos); c.homeUp.copy(c.up); this.setState(c, 'IDLE'); } }
        // stuck against something it cannot climb: sidestep for a moment
        if (d < c.bestD - 0.1) { c.bestD = d; c.stuckT = 0; } else c.stuckT += dt;
        if (c.stuckT > 2) { c.stuckT = -1; c.bestD = 1e9; c.wanderDir.crossVectors(c.up, dir).normalize(); }
        if (c.stuckT < 0) dir.copy(c.wanderDir);
        if (Game.time - c.heardT > U1.CRAWLER_GIVE_UP_TIME) this.setState(c, 'IDLE');
        break;
      }
      case 'FLINCH': case 'FLEE': {
        speed = U1.CRAWLER_SPEED_FLEE;
        dir.copy(c.pos).sub(c.fleeFrom);
        if (c.stateT > (c.state === 'FLINCH' ? U1.CRAWLER_FLINCH_TIME : 2.5)) this.setState(c, Game.time - c.heardT < 3 ? 'STALK' : 'IDLE');
        break;
      }
      case 'STUN': {   // on its back, legs twitching
        if (c.stateT > U1.CRAWLER_STUN_TIME) this.setState(c, 'FLEE', Player.head);
        break;
      }
    }
    if (speed > 0) this.crawl(c, dir, speed, dt);
    c.speed = damp(c.speed, speed, 10, dt);
    this.animate(c, dt, c.speed);
  },
  turnToward(c, dir, dt) {
    _ca.copy(dir);
    this.tangent(c, _ca);
    c.fwd.lerp(_ca, 1 - Math.exp(-6 * dt));
    this.tangent(c, c.fwd);
  },

  // Walk along any surface: climb onto walls ahead, stick to what is below, wrap over edges, else fall.
  crawl(c, dirIn, speed, dt) {
    const BH = U1.CRAWLER_BODY_HEIGHT;
    _ca.copy(dirIn);
    if (_ca.lengthSq() < 1e-8) return;
    this.tangent(c, _ca);
    c.fwd.lerp(_ca, 1 - Math.exp(-8 * dt));
    this.tangent(c, c.fwd);
    const step = speed * dt;
    // 1. a surface ahead: climb onto it (the old "up" becomes the new "forward")
    if (World.raycastHit(c.pos, c.fwd, step + 0.2, this._filter, _cHit) && _cHit.normal.dot(c.up) < 0.7) {
      _cc.copy(c.up);
      c.up.copy(_cHit.normal);
      c.fwd.copy(_cc);
      this.tangent(c, c.fwd);
      c.pos.copy(_cHit.point).addScaledVector(c.up, BH);
      return;
    }
    c.pos.addScaledVector(c.fwd, step);
    // 2. stick to the surface underneath
    _cb.copy(c.pos).addScaledVector(c.up, 0.12);
    _cc.copy(c.up).negate();
    if (World.raycastHit(_cb, _cc, 0.12 + BH + 0.3, this._filter, _cHit)) {
      c.pos.copy(_cHit.point).addScaledVector(_cHit.normal, BH);
      c.up.lerp(_cHit.normal, 1 - Math.exp(-14 * dt)).normalize();
      return;
    }
    // 3. walked off an edge: wrap around it onto the face below
    _cb.copy(c.pos).addScaledVector(c.up, -(BH + 0.12));
    _cc.copy(c.fwd).negate();
    if (World.raycastHit(_cb, _cc, 0.6, this._filter, _cHit) && _cHit.normal.dot(c.up) < 0.7) {
      _ce.copy(c.up);
      c.up.copy(_cHit.normal);
      c.fwd.copy(_ce).negate();
      this.tangent(c, c.fwd);
      c.pos.copy(_cHit.point).addScaledVector(c.up, BH);
      return;
    }
    // 4. nothing underneath: fall
    c.airborne = true; c.vel.copy(c.fwd).multiplyScalar(speed * 0.5);
  },
  fly(c, dt) {
    c.vel.y += CONFIG.GRAVITY * dt;
    const L = c.vel.length() * dt;
    if (L > 1e-6) {
      _ca.copy(c.vel).normalize();
      if (World.raycastHit(c.pos, _ca, L + U1.CRAWLER_BODY_HEIGHT, this._filter, _cHit)) {
        // land feet-first on whatever it hit
        c.airborne = false;
        c.up.copy(_cHit.normal);
        c.pos.copy(_cHit.point).addScaledVector(c.up, U1.CRAWLER_BODY_HEIGHT);
        c.fwd.copy(c.vel); this.tangent(c, c.fwd);
        c.vel.set(0, 0, 0);
        if (c.state === 'LUNGE') { this.setState(c, 'STALK'); c.heardT = Game.time - 1.5; c.heardPlayer = false; }
        else if (c.state === 'STUN') { c.stateT = 0; AudioSys.impact('STICKY', c.pos, 1.5); }
        return;
      }
      c.pos.addScaledVector(c.vel, dt);
    }
    if (c.state === 'LUNGE' && Game.state === 'PLAYING') {
      // latch onto a hand it hits (or the nearest hand if it hits your face)
      let best = null, bd = U1.CRAWLER_CLING_RADIUS;
      for (const h of Player.hands) { const d = h.phys.distanceTo(c.pos); if (d < bd && !h.cling) { bd = d; best = h; } }
      if (!best && c.pos.distanceTo(Player.head) < 0.45) best = Player.hands[0].cling ? (Player.hands[1].cling ? null : Player.hands[1]) : Player.hands[0];
      if (best) this.cling(c, best);
    }
    const killY = Level.data && Level.data.killY !== undefined ? Level.data.killY : -40;
    if (c.pos.y < killY || c.stateT > 12) this.remove(c);
  },
  lunge(c, target) {
    // a hand still near the sound is what it leaps at
    let aim = target;
    for (const h of Player.hands) if (h.phys.distanceTo(target) < 0.6) aim = h.phys;
    this.setState(c, 'LUNGE');
    const T = U1.CRAWLER_LUNGE_TIME;
    c.vel.copy(aim).sub(c.pos).multiplyScalar(1 / T); c.vel.y -= 0.5 * CONFIG.GRAVITY * T;
    c.airborne = true; c.jawT = 1;
    c.pos.addScaledVector(c.up, 0.05);
    AudioSys.shriek(c.pos, 0.6);
    Subtitles.add('[SHRIEK]', c.pos, 'crawlshriek');
  },

  // ------------------------------------------------------------ CLING
  cling(c, h) {
    if (h.anchored) Player.release(h, false);
    if (h.holding) Grab.drop(h);
    if (h.cord) Cords.letGo(h.cord);
    c.state = 'CLING'; c.stateT = 0; c.airborne = false; c.hand = h; h.cling = c;
    c.shakes = 0; c.shakeArmed = true; c.lastShakeT = -99; c.shriekT = 0.4; c.litT = 0;
    Input.haptic(h.side, 1, 220);
    Game.toast('CRAWLER! SHAKE IT OFF');
    AudioSys.shriek(c.pos, 1);
  },
  updateCling(c, dt) {
    const h = c.hand;
    // wrapped over the back of the hand
    c.up.set(0, 1, 0).applyQuaternion(h.worldQuat);
    c.fwd.set(0, 0, -1).applyQuaternion(h.worldQuat);
    c.pos.copy(h.phys).addScaledVector(c.up, 0.07).addScaledVector(c.fwd, -0.02);
    // it shrieks every second: a LOUD noise the Warden hears
    c.shriekT -= dt;
    if (c.shriekT <= 0) {
      c.shriekT = U1.CRAWLER_SHRIEK_INTERVAL; c.jawT = 1;
      AudioSys.shriek(c.pos, 1);
      Game.noise(c.pos, U1.CRAWLER_SHRIEK_LOUDNESS, 'crawler');
      Subtitles.add('[SHRIEKING — on your hand]', null, 'clingshriek');
    } else if (c.shriekT < U1.CRAWLER_SHRIEK_INTERVAL - 0.35) c.jawT = 0.25;
    Input.haptic(h.side, 0.2 + Math.random() * 0.25, 25);
    // shake it off: three fast swings of that arm (desktop: X)
    const sp = Input.xr || !Input.desktopActive ? h.relVel.length() : (Input.shakePulse ? 99 : 0);
    if (sp > U1.CRAWLER_SHAKE_SPEED && c.shakeArmed) {
      c.shakeArmed = false; c.shakes++; c.lastShakeT = Game.time;
      Input.haptic(h.side, 0.8, 40);
      if (c.shakes >= U1.CRAWLER_SHAKES_TO_REMOVE) { this.shakeOff(c); return; }
    } else if (sp < U1.CRAWLER_SHAKE_SPEED * 0.5) c.shakeArmed = true;
    if (Game.time - c.lastShakeT > U1.CRAWLER_SHAKE_RESET) c.shakes = 0;
    this.animate(c, dt, 0.6);
  },
  shakeOff(c) {
    const h = c.hand;
    this.detach(c);
    c.state = 'STUN'; c.stateT = 0; c.airborne = true;
    if (Input.xr || !Input.desktopActive) c.vel.copy(h.relVel).multiplyScalar(1.4);
    else c.vel.set(0, 0, -4).applyQuaternion(Player.headWorldQuat);
    if (c.vel.length() < 3) c.vel.setLength(3.5);
    c.vel.y += 1.5;
    c.pos.addScaledVector(c.vel, 0.03);
    AudioSys.chitter(c.pos, 0.8);
    Game.onCrawlerRemoved();
  },

  // ------------------------------------------------------------ flashlight: it feels the heat
  flashCheck(dt) {
    const on = Flashlight.on && Flashlight.light.intensity > 1;
    if (on && this.lit > 0) Flashlight.battery = Math.max(0, Flashlight.battery - U1.CRAWLER_FLASH_DRAIN * dt * Math.min(this.lit, 3));
    this.flashT -= dt;
    if (this.flashT > 0) return;
    this.flashT = 0.2; this.lit = 0;
    if (!on) return;
    const F = Flashlight.light.position, D = Flashlight.beamDir, cosA = Math.cos(CONFIG.FLASH_ANGLE * 1.1);
    for (let i = this.list.length - 1; i >= 0; i--) {
      const c = this.list[i];
      if (c.state === 'STUN' || c.airborne) continue;
      _ca.copy(c.pos).sub(F);
      const d = _ca.length();
      if (d > CONFIG.FLASH_DISTANCE * 0.6 || d < 0.05) continue;
      _ca.divideScalar(d);
      if (_ca.dot(D) < cosA) continue;
      if (c.state !== 'CLING' && World.raycast(F, _ca, Math.max(0, d - 0.25), null, null)) continue;
      this.lit++;
      if (c.state === 'CLING') { c.litT += 0.2; if (c.litT > 0.6) this.shakeOff(c); continue; }
      if (c.state !== 'FLINCH') { this.setState(c, 'FLINCH', F); AudioSys.chitter(c.pos, 0.7); }
      else c.stateT = Math.min(c.stateT, 0.5);
    }
  },

  // ------------------------------------------------------------ animation
  frame(c) {
    _cs.crossVectors(c.up, c.fwd).normalize();
    _cm.makeBasis(_cs, c.up, c.fwd);
    c.quat.setFromRotationMatrix(_cm);
    if (c.state === 'STUN' && !c.airborne) c.quat.multiply(_cq.setFromAxisAngle(ZAXIS, Math.PI));   // on its back
    c.bodyPos.copy(c.pos).addScaledVector(c.up, c.bob);
  },
  footIdeal(c, i, speed, out) {
    const H = CRAWLER_HIPS[i];
    if (c.state === 'CLING') return out.set(H[0] * 1.3, -0.07, H[2] * 1.1).applyQuaternion(c.quat).add(c.pos);   // legs wrapped round the hand
    if (c.airborne) return out.set(H[0] * 2.2, 0.02 + Math.sin(Game.time * 30 + i) * 0.04, H[2] * 1.9).applyQuaternion(c.quat).add(c.pos);   // flailing
    return out.set(H[0] * 1.9, -U1.CRAWLER_BODY_HEIGHT, H[2] * 1.7 + speed * 0.05).applyQuaternion(c.quat).add(c.pos);
  },
  animate(c, dt, speed) {
    c.jaw = damp(c.jaw, c.jawT + (c.state === 'LISTEN' ? Math.sin(Game.time * 30) * 0.05 : 0), 18, dt);
    if (c.state !== 'CLING' && c.state !== 'LUNGE') c.jawT = damp(c.jawT, 0.1, 2, dt);
    // twitchy, insect-like head
    c.jitterT -= dt;
    if (c.jitterT <= 0) {
      c.jitterT = 0.05 + Math.random() * (c.state === 'LISTEN' ? 0.12 : 0.3);
      c.jitter.set((Math.random() - 0.5) * 0.5 - (c.state === 'LISTEN' ? 0.35 : 0), (Math.random() - 0.5) * 0.7, (Math.random() - 0.5) * 0.4);
    }
    c.headJ.lerp(c.jitter, 1 - Math.exp(-25 * dt));
    c.gaitT += dt * (speed > 0.02 ? 6 + speed * 10 : 0);
    c.bob = Math.sin(c.gaitT * 2) * 0.012 * Math.min(1, speed * 2);
    this.frame(c);
    // tripod gait: one tripod steps while the other holds
    for (let i = 0; i < 6; i++) {
      const f = c.feet[i], g = CRAWLER_TRIPOD[i];
      this.footIdeal(c, i, speed, _ca);
      if (c.airborne || c.state === 'CLING') { f.pos.lerp(_ca, 1 - Math.exp(-20 * dt)); if (f.stepping) { f.stepping = false; c.tri[g]--; } continue; }
      if (!f.stepping) {
        if (f.pos.distanceTo(_ca) > (speed > 0.02 ? 0.07 : 0.11) && c.tri[1 - g] === 0) { f.from.copy(f.pos); f.t = 0; f.stepping = true; c.tri[g]++; }
      }
      if (f.stepping) {
        f.to.copy(_ca);
        f.t += dt / (0.06 + 0.06 / (1 + speed * 3));
        if (f.t >= 1) { f.t = 1; f.stepping = false; c.tri[g]--; }
        f.pos.lerpVectors(f.from, f.to, f.t).addScaledVector(c.up, Math.sin(Math.PI * f.t) * 0.045);
      }
    }
    // head and jaws
    c.headPos.set(0, 0.03, 0.2).applyQuaternion(c.quat).add(c.bodyPos);
    c.headQuat.copy(c.quat).multiply(_cq.setFromEuler(_cr.set(c.headJ.x, c.headJ.y, c.headJ.z)));
  },

  render() {
    const M = this.meshes;
    if (!M) return;
    const blob = Game.progress.settings.arachnophobia;
    let n = 0, nj = 0, nl = 0;
    for (const c of this.list) {
      if (blob) {   // arachnophobia mode: same creature, drawn as a soft pulsing light
        const s = 1 + Math.sin(Game.time * 6 + n) * 0.12 + (c.state === 'CLING' ? 0.25 : 0);
        M.blob.setMatrixAt(n++, _cm.compose(c.bodyPos, c.quat, _cs.set(s, s * 0.8, s)));
        continue;
      }
      M.body.setMatrixAt(n, _cm.compose(c.bodyPos, c.quat, ONE3));
      M.head.setMatrixAt(n, _cm.compose(c.headPos, c.headQuat, ONE3));
      const open = 0.06 + c.jaw * 0.55;
      for (const s of [-1, 1]) {
        _ca.set(s * 0.022, -0.012, 0.07).applyQuaternion(c.headQuat).add(c.headPos);
        _cq.copy(c.headQuat).multiply(_cq2.setFromAxisAngle(UP, s * open));   // the halves swing apart sideways
        if (s > 0) _cq.multiply(JAW_FLIP);                                     // right half: the same plate turned over
        M.jaw.setMatrixAt(nj++, _cm.compose(_ca, _cq, ONE3));
      }
      for (let i = 0; i < 6; i++) {
        const H = CRAWLER_HIPS[i], f = c.feet[i].pos;
        const hip = _cb.set(H[0], 0.0, H[2]).applyQuaternion(c.quat).add(c.bodyPos);
        // knee: above the midpoint, pushed outward
        const knee = _cc.copy(hip).add(f).multiplyScalar(0.5).addScaledVector(c.up, 0.09);
        _ce.set(H[0], 0, 0).applyQuaternion(c.quat); knee.addScaledVector(_ce, 0.35);
        nl = this.segment(M.leg, nl, hip, knee, 0.014);
        nl = this.segment(M.leg, nl, knee, f, 0.009);
      }
      n++;
    }
    M.body.count = blob ? 0 : n; M.head.count = blob ? 0 : n; M.jaw.count = nj; M.leg.count = nl; M.blob.count = blob ? n : 0;
    for (const k in M) if (M[k].count) M[k].instanceMatrix.needsUpdate = true;
  },
  // a leg segment from a to b (unit cylinder hangs along -Y)
  segment(mesh, idx, a, b, r) {
    _cd.copy(b).sub(a);
    const len = _cd.length();
    if (len < 1e-5) return idx;
    _cq.setFromUnitVectors(DOWN, _cd.multiplyScalar(1 / len));
    mesh.setMatrixAt(idx, _cm.compose(a, _cq, _cs.set(r, len, r)));
    return idx + 1;
  },

  // ------------------------------------------------------------ sound
  // The three nearest moving Crawlers each drive a looping skitter voice.
  sounds(dt, playing) {
    const near = this.near;
    near[0] = near[1] = near[2] = null;
    const H = Player.head;
    for (const c of this.list) {
      if (c.airborne || c.state === 'CLING' || c.speed < 0.05) continue;
      const d = c.pos.distanceToSquared(H);
      if (!near[0] || d < near[0].pos.distanceToSquared(H)) { near[2] = near[1]; near[1] = near[0]; near[0] = c; }
      else if (!near[1] || d < near[1].pos.distanceToSquared(H)) { near[2] = near[1]; near[1] = c; }
      else if (!near[2] || d < near[2].pos.distanceToSquared(H)) near[2] = c;
    }
    const soft = Game.progress.settings.arachnophobia ? 0.4 : 1;
    for (let i = 0; i < 3; i++) {
      const c = playing ? near[i] : null;
      if (!c) { AudioSys.setSkitter(i, 0, null); continue; }
      const v = 0.22 * soft * clamp(c.speed / U1.CRAWLER_SPEED_STALK, 0.3, 1.4) * (Math.random() < 0.5 ? 1 : 0.2);   // rapid filtered clicks
      AudioSys.setSkitter(i, v, c.pos);
    }
    this.subT -= dt;
    if (playing && near[0] && this.subT <= 0 && near[0].pos.distanceTo(H) < 9) { this.subT = 1; Subtitles.add('[skittering]', near[0].pos, 'skitter'); }
    for (const c of this.list) {
      c.chitterT -= dt;
      if (c.chitterT <= 0) { c.chitterT = 4 + Math.random() * 8; if (playing && c.state === 'IDLE' && c.pos.distanceTo(H) < 14) AudioSys.chitter(c.pos, 0.3); }
    }
```

## PATCH #62 — 8. INTERACTABLES: a lantern on a path that does not exist yet waits for its stage

FIND:
```js
    addCollider(this, World.makeBox(_iv.copy(this.pos).setY(this.pos.y + 0.22), null, _iw.set(0.13, 0.22, 0.13)));
    this.lit = false; this.t = Math.random() * 10;
  }
  respawnPos(out) { return out.copy(this.pos).addScaledVector(this.spawnDir, 0.75).setY(this.pos.y + 0.9); }
```
REPLACE WITH:
```js
    addCollider(this, World.makeBox(_iv.copy(this.pos).setY(this.pos.y + 0.22), null, _iw.set(0.13, 0.22, 0.13)));
    this.lit = false; this.t = Math.random() * 10;
    // UPDATE 1: a lantern on a path that does not exist yet waits for its stage
    this.stage = def.stage || null; this.dormant = !!def.stage;
    if (this.dormant) { this.group.visible = false; this.colliders[0].enabled = false; }
  }
  wakeUp() { this.dormant = false; this.group.visible = true; this.colliders[0].enabled = true; }
  respawnPos(out) { return out.copy(this.pos).addScaledVector(this.spawnDir, 0.75).setY(this.pos.y + 0.9); }
```

## PATCH #63 — 8. INTERACTABLES: edit: if (this.dormant) return;

INSERT AFTER:
```js
  near(p, r) { return _iv.copy(this.pos).setY(this.pos.y + 0.22).distanceTo(p) < r; }
  update(dt) {
    if (!this.lit) {
```
NEW CODE:
```js
    if (this.dormant) return;
```

## PATCH #64 — 8. INTERACTABLES: UPDATE 1

INSERT AFTER:
```js
      Game.setCheckpoint(this);
      if (this.objective) Game.objectiveProgress('lantern');
    }
```
NEW CODE:
```js
      Achievements.award('firstlight');   // UPDATE 1
```

## PATCH #65 — 8. INTERACTABLES: 'chapelbell' = The Flooded Chapel's great bell

FIND:
```js
    this.hang = new THREE.Vector3().fromArray(def.p);
    this.len = def.len || 1.4;
    const g = this.group; g.position.copy(this.hang);
    propMesh(colorizeGeometry(new THREE.CylinderGeometry(0.025, 0.025, this.len, 5), 0xa08a60), getMaterial('rope'), g, 0, -this.len / 2, 0);
    const pts = [];
    for (let i = 0; i <= 10; i++) { const t = i / 10; pts.push(new THREE.Vector2(0.06 + 0.3 * Math.pow(t, 1.6) + (t > 0.9 ? 0.05 : 0), -t * 0.62)); }
    this.bellMat = new THREE.MeshLambertMaterial({ color: 0x9a7a3a, emissive: 0x000000, side: THREE.DoubleSide });
    const bell = propMesh(new THREE.LatheGeometry(pts, 14), this.bellMat, g, 0, -this.len, 0);
    propMesh(new THREE.SphereGeometry(0.07, 8, 6), PropMat.lambert(0x3a3020, 'clapper'), g, 0, -this.len - 0.55, 0);
    this.bell = bell;
    this.center = new THREE.Vector3().copy(this.hang).add(_iv.set(0, -this.len - 0.32, 0));
    addCollider(this, World.makeCyl(this.center, null, 0.34, 0.32, 'NOISY'));
    this.angX = 0; this.angZ = 0; this.velX = 0; this.velZ = 0; this.glow = 0; this.rung = false; this.cool = 0;
```
REPLACE WITH:
```js
    this.hang = new THREE.Vector3().fromArray(def.p);
    this.len = def.len || 1.4;
    this.kind = def.kind || 'bell';   // UPDATE 1: 'chapelbell' = The Flooded Chapel's great bell
    const S = this.size = def.size || 1;
    const g = this.group; g.position.copy(this.hang);
    propMesh(colorizeGeometry(new THREE.CylinderGeometry(0.025, 0.025, this.len, 5), 0xa08a60), getMaterial('rope'), g, 0, -this.len / 2, 0);
    const pts = [];
    for (let i = 0; i <= 10; i++) { const t = i / 10; pts.push(new THREE.Vector2((0.06 + 0.3 * Math.pow(t, 1.6) + (t > 0.9 ? 0.05 : 0)) * S, -t * 0.62 * S)); }
    this.bellMat = new THREE.MeshLambertMaterial({ color: 0x9a7a3a, emissive: 0x000000, side: THREE.DoubleSide });
    const bell = propMesh(new THREE.LatheGeometry(pts, 14), this.bellMat, g, 0, -this.len, 0);
    propMesh(new THREE.SphereGeometry(0.07 * S, 8, 6), PropMat.lambert(0x3a3020, 'clapper'), g, 0, -this.len - 0.55 * S, 0);
    this.bell = bell;
    this.center = new THREE.Vector3().copy(this.hang).add(_iv.set(0, -this.len - 0.32 * S, 0));
    addCollider(this, World.makeCyl(this.center, null, 0.34 * S, 0.32 * S, 'NOISY'));
    this.angX = 0; this.angZ = 0; this.velX = 0; this.velZ = 0; this.glow = 0; this.rung = false; this.cool = 0;
```

## PATCH #66 — 8. INTERACTABLES: edit: AudioSys.bell(this.center, clamp(speed / 2, 0.5, 1), this.kind === 'ch…

FIND:
```js
    if (this.cool > 0) return;
    this.cool = 0.4;
    AudioSys.bell(this.center, clamp(speed / 2, 0.5, 1));
    Game.noise(this.center, 18);
```
REPLACE WITH:
```js
    if (this.cool > 0) return;
    this.cool = 0.4;
    AudioSys.bell(this.center, clamp(speed / 2, 0.5, 1), this.kind === 'chapelbell' ? 131 : 262);
    Subtitles.add('[a bell rings]', this.center);
    Game.noise(this.center, 18);
```

## PATCH #67 — 8. INTERACTABLES: edit: if (!this.rung) { this.rung = true; Game.objectiveProgress(this.kind);…

FIND:
```js
    this.glow = 1;
    if (h) Input.haptic(h.side, 1, 200);
    if (!this.rung) { this.rung = true; Game.objectiveProgress('bell'); }
  }
```
REPLACE WITH:
```js
    this.glow = 1;
    if (h) Input.haptic(h.side, 1, 200);
    if (!this.rung) { this.rung = true; Game.objectiveProgress(this.kind); Game.onBellRung(this.kind); }
  }
```

## PATCH #68 — 8. INTERACTABLES: a glowing stone from the Nest

INSERT AFTER:
```js
      this.light.position.y = 0.2; this.group.add(this.light);
      if (Game.progress.toys[Game.levelIndex]) this.inner.traverse((o) => { if (o.material) o.material = PropMat.lambert(0x6a5a4a, 'toyFound'); });
    }
```
NEW CODE:
```js
    } else if (this.type === 'gem') {   // UPDATE 1: a glowing stone from the Nest
      propMesh(new THREE.OctahedronGeometry(0.09, 0), PropMat.basic(0x70ffd8, 'gemGlow'), this.inner, 0, 0.12, 0).scale.set(0.8, 1.3, 0.8);
      propMesh(new THREE.OctahedronGeometry(0.05, 0), PropMat.basic(0xd8fff4, 'gemCore'), this.inner, 0.06, 0.07, 0.02);
      this.light = new THREE.PointLight(0x60ffd0, 0.9 * CONFIG.LIGHT_SCALE, 4, 1.8);
      this.light.position.y = 0.15; this.group.add(this.light);
```

## PATCH #69 — 8. INTERACTABLES: edit: AudioSys.chime(this.pos, 0.45, this.type === 'toy' ? 660 : this.type =…

FIND:
```js
    this.group.visible = false;
    if (this.light) this.light.intensity = 0;
    AudioSys.chime(this.pos, 0.45, this.type === 'toy' ? 660 : 990);
    Input.hapticBoth(0.35, 80);
```
REPLACE WITH:
```js
    this.group.visible = false;
    if (this.light) this.light.intensity = 0;
    AudioSys.chime(this.pos, 0.45, this.type === 'toy' ? 660 : this.type === 'gem' ? 1320 : 990);
    Input.hapticBoth(0.35, 80);
```

## PATCH #70 — 8. INTERACTABLES: a rock slab that grinds aside

FIND:
```js
    } else if (this.type === 'rim') {
      this.isOpen = true; this.anim = 1;
    }
    for (const c of this.colliders) c.blocksWarden = this.type === 'gate' || this.type === 'finalGate';
  }
```
REPLACE WITH:
```js
    } else if (this.type === 'rim') {
      this.isOpen = true; this.anim = 1;
    } else if (this.type === 'rockdoor') {   // UPDATE 1: a rock slab that grinds aside
      const w = def.w || 3.2, h = def.h || 4;
      propMesh(new THREE.PlaneGeometry(w, h), PropMat.basic(0x000000, 'holeBlack'), g, 0, h / 2, -0.4);
      const slab = colorizeGeometry(new THREE.BoxGeometry(w + 0.4, h + 0.3, 0.7), 0x6a645c, 0.15);
      worldUV(slab, 2);
      propMesh(slab, getMaterial('rock'), this.moving, 0, h / 2, 0);
      this.col = addCollider(this, World.makeBox(L(0, h / 2, 0), q, _iw.set(w / 2 + 0.2, h / 2 + 0.15, 0.35)));
      this.slideW = w + 0.6;
    } else if (this.type === 'pit') {        // UPDATE 1: a ragged hole into the dark
      this.isOpen = true; this.anim = 1;
      const r = def.r || 1.4;
      const hole = propMesh(new THREE.CircleGeometry(r, 18), PropMat.basic(0x000000, 'holeBlack'), g, 0, 0.015, 0);
      hole.rotation.x = -Math.PI / 2;
      const rim = [];
      for (let i = 0; i < 14; i++) {
        const a = i / 14 * Math.PI * 2, rr = r + 0.15 + Math.random() * 0.25;
        rim.push([colorizeGeometry(new THREE.BoxGeometry(0.4 + Math.random() * 0.4, 0.12 + Math.random() * 0.15, 0.3 + Math.random() * 0.3), 0x3a3028), Math.cos(a) * rr, 0.05, Math.sin(a) * rr, Math.random() * 0.4, -a, Math.random() * 0.3]);
      }
      mergeInto(g, getMaterial('rock'), rim);
    }
    for (const c of this.colliders) c.blocksWarden = this.type === 'gate' || this.type === 'finalGate' || this.type === 'rockdoor';
  }
```

## PATCH #71 — 8. INTERACTABLES: edit: else if (this.type === 'rockdoor') this.moving.position.x = a * this.s…

INSERT AFTER:
```js
      else if (this.type === 'gate' || this.type === 'finalGate') this.moving.position.y = a * (this.gateH + 0.3);
      else if (this.type === 'elevator') { this.moving.position.z = a * 2.9; if (this.cageLight) this.cageLight.intensity = a * 2 * CONFIG.LIGHT_SCALE; }
      if (this.col) this.col.enabled = a < 0.5;
```
NEW CODE:
```js
      else if (this.type === 'rockdoor') this.moving.position.x = a * this.slideW;
```

## PATCH #72 — 8. INTERACTABLES: UPDATE 1

INSERT AFTER:
```js
    if (P.x > this.trigMin.x && P.x < this.trigMax.x && P.y > this.trigMin.y && P.y < this.trigMax.y && P.z > this.trigMin.z && P.z < this.trigMax.z) {
      if (this.type === 'finalGate') Game.onFinalGate(this);
      else Game.levelComplete();
```
NEW CODE:
```js
      else if (this.type === 'pit') Game.onPit(this);   // UPDATE 1
```

## PATCH #73 — 8. INTERACTABLES: slammed platforms come back on respawn

FIND:
```js
    if (this.t > 2.5) this.mesh.visible = false;
  }
  reset() {}
}
```
REPLACE WITH:
```js
    if (this.t > 2.5) this.mesh.visible = false;
  }
  reset() {
    if (!this.resettable || !this.collapsed || !this.mesh) return;   // UPDATE 1: slammed platforms come back on respawn
    this.collapsed = false; this.t = 0; this.vel = 0;
    this.mesh.position.copy(this.center); this.mesh.rotation.set(0, 0, 0); this.mesh.visible = true;
    for (const c of this.colliders) c.enabled = true;
  }
}
```

## PATCH #74 — 8. INTERACTABLES: whole section: 8b. UPDATE 1 SYSTEMS — subtitles, achievements, cosmetics,

FIND:
```js
const Interact = {
  list: [], lanterns: [], crumbles: [], lamps: [], roofs: [], valves: [], bells: [], exit: null, generator: null,
  clear() {
    this.list.length = 0; this.lanterns.length = 0; this.crumbles.length = 0; this.lamps.length = 0; this.roofs.length = 0;
    this.valves.length = 0; this.bells.length = 0; this.exit = null; this.generator = null;
  },
  add(o) { this.list.push(o); return o; },
  update(dt) { for (let i = 0; i < this.list.length; i++) this.list[i].update(dt); },
  resetForRespawn() { for (const c of this.crumbles) c.reset(); },
};
```
REPLACE WITH:
```js
const Interact = {
  list: [], lanterns: [], crumbles: [], lamps: [], roofs: [], valves: [], bells: [], exit: null, generator: null,
  slams: [],   // UPDATE 1: slammable platforms
  clear() {
    this.list.length = 0; this.lanterns.length = 0; this.crumbles.length = 0; this.lamps.length = 0; this.roofs.length = 0;
    this.valves.length = 0; this.bells.length = 0; this.exit = null; this.generator = null;
    this.slams.length = 0;
  },
  add(o) { this.list.push(o); return o; },
  update(dt) { for (let i = 0; i < this.list.length; i++) this.list[i].update(dt); },
  resetForRespawn() { for (const c of this.crumbles) c.reset(); for (const s of this.slams) s.reset(); },
};

/* =====================================================================
   8b. UPDATE 1 SYSTEMS — subtitles, achievements, cosmetics,
       throwables & flares, hiding spots, rising water
   ===================================================================== */
const _gv = new THREE.Vector3(), _gw = new THREE.Vector3(), _gp = new THREE.Vector3(), _gn = new THREE.Vector3(), _gt = new THREE.Vector3();
const _gq = new THREE.Quaternion(), _gm = new THREE.Matrix4();

// --------------------------------------------------------------- Subtitles: "[heavy footsteps — left]"
const Subtitles = {
  panel: null, lines: [], last: new Map(), dirty: false,
  init(camera) {
    this.panel = new CanvasPanel(0.62, 0.13, 1024, 214, { depthTest: false, renderOrder: 992 });
    this.panel.mesh.position.set(0, -0.27, -0.85); this.panel.mesh.visible = false;
    camera.add(this.panel.mesh);
  },
  add(text, pos, key) {
    if (!Game.progress.settings.subtitles) return;
    const k = key || text, now = Game.time;
    if (now - (this.last.get(k) || -99) < U1.SUBTITLE_REPEAT) return;
    this.last.set(k, now);
    const label = pos ? text.slice(0, -1) + ' — ' + this.direction(pos) + ']' : text;
    for (const l of this.lines) if (l.key === k) { l.text = label; l.t = U1.SUBTITLE_TIME; this.dirty = true; return; }
    this.lines.push({ text: label, t: U1.SUBTITLE_TIME, key: k });
    if (this.lines.length > 3) this.lines.shift();
    this.dirty = true;
  },
  direction(pos) {
    _gv.copy(pos).sub(Player.head);
    const horiz = Math.hypot(_gv.x, _gv.z);
    if (_gv.y > 2 && _gv.y > horiz * 1.2) return 'above';
    if (_gv.y < -2 && -_gv.y > horiz * 1.2) return 'below';
    _gw.set(0, 0, -1).applyQuaternion(Player.headWorldQuat);
    const f = _gv.x * _gw.x + _gv.z * _gw.z, r = -_gv.x * _gw.z + _gv.z * _gw.x;
    if (Math.abs(r) > Math.abs(f) * 0.7) return r > 0 ? 'right' : 'left';
    return f > 0 ? 'ahead' : 'behind';
  },
  clear() { this.lines.length = 0; this.dirty = true; },
  update(dt) {
    for (let i = this.lines.length - 1; i >= 0; i--) { this.lines[i].t -= dt; if (this.lines[i].t <= 0) { this.lines.splice(i, 1); this.dirty = true; } }
    if (!Game.progress.settings.subtitles && this.lines.length) { this.lines.length = 0; this.dirty = true; }
    if (!this.dirty) return;
    this.dirty = false;
    this.panel.mesh.visible = this.lines.length > 0;
    if (!this.lines.length) return;
    this.panel.draw((c, W, H) => {
      c.font = 'bold 50px Georgia'; c.textAlign = 'center'; c.textBaseline = 'middle';
      this.lines.forEach((l, i) => {
        const y = H - 40 - (this.lines.length - 1 - i) * 66, w = c.measureText(l.text).width + 40;
        c.fillStyle = 'rgba(0,0,0,0.7)'; c.fillRect(W / 2 - w / 2, y - 30, w, 60);
        c.fillStyle = '#f4ecd8'; c.fillText(l.text, W / 2, y + 2);
      });
    });
  },
};

// --------------------------------------------------------------- Achievements
const ACHIEVEMENTS = [
  { id: 'firstlight', name: 'FIRST LIGHT', hint: 'Light a lantern' },
  { id: 'neverseen', name: 'NEVER SEEN', hint: 'Finish a level the Warden hunts in without it ever hunting you' },
  { id: 'bellringer', name: 'BELL RINGER', hint: 'Ring the three Canopy bells and the chapel bell' },
  { id: 'shakeitoff', name: 'SHAKE IT OFF', hint: 'Shake off 10 Crawlers' },
  { id: 'deepsleeper', name: 'DEEP SLEEPER', hint: 'Finish The Nest without waking the Warden' },
  { id: 'escapee', name: 'ESCAPEE', hint: 'Reach the lighthouse gate' },
  { id: 'trueending', name: 'TRUE ENDING', hint: 'Cut the last cord' },
  { id: 'toybox', name: 'TOY BOX', hint: 'Find all 9 carved toys' },
  { id: 'archivist', name: 'ARCHIVIST', hint: 'Find all 18 notes' },
  { id: 'bait', name: 'BAIT', hint: 'Lure the Warden with something you threw' },
  { id: 'heldbreath', name: 'HELD BREATH', hint: 'Stay hidden 5 s with the Warden right outside' },
  { id: 'nightmare', name: 'NIGHTMARE', hint: 'Finish any level in Nightmare' },
  { id: 'deepdiver', name: 'DEEP DIVER', hint: 'Reach floor 10 of the Endless Descent' },
  { id: 'quickhands', name: 'QUICK HANDS', hint: 'Set a Time Trial record' },
];
const Achievements = {
  has(id) { return !!Game.progress.achievements[id]; },
  count() { let n = 0; for (const a of ACHIEVEMENTS) if (Game.progress.achievements[a.id]) n++; return n; },
  award(id) {
    if (this.has(id)) return;
    Game.progress.achievements[id] = true;
    Game.saveProgress();
    const def = ACHIEVEMENTS.find((a) => a.id === id);
    UI.toast('ACHIEVEMENT: ' + (def ? def.name : id));
    AudioSys.chime(null, 0.4, 1320);
    Input.hapticBoth(0.3, 80);
    Hub.refreshBoard();
    UI.refreshSettings();
  },
  checkCollections() {
    const P = Game.progress;
    if (P.toys.every(Boolean)) this.award('toybox');
    if (P.notes.every(Boolean)) this.award('archivist');
    if (P.stats.crawlersRemoved >= 10) this.award('shakeitoff');
    if (P.stats.canopyBells && P.stats.chapelBell) this.award('bellringer');
  },
};

// --------------------------------------------------------------- Cosmetics (unlocked by toys, chosen at the Shelf)
const COSMETICS = [
  { id: 'fur_default', kind: 'fur', name: 'DARK FUR', toys: 0, tex: 'hair' },
  { id: 'fur_pale', kind: 'fur', name: 'PALE FUR', toys: 1, tex: 'furPale' },
  { id: 'fur_ember', kind: 'fur', name: 'EMBER FUR', toys: 2, tex: 'furEmber' },
  { id: 'bracelet', kind: 'bracelet', name: 'BELL BRACELET', toys: 3 },
  { id: 'fur_striped', kind: 'fur', name: 'STRIPED FUR', toys: 4, tex: 'furStriped' },
  { id: 'lantern', kind: 'lantern', name: 'LANTERN LIGHT', toys: 5 },
  { id: 'fur_moss', kind: 'fur', name: 'MOSS FUR', toys: 6, tex: 'furMoss' },
  { id: 'fur_ghost', kind: 'fur', name: 'GHOST FUR', toys: 7, tex: 'furGhost' },
  { id: 'crown', kind: 'crown', name: 'CROWN', toys: 9 },
];
const Cosmetics = {
  bracelet: null, lanternModel: null,
  toys() { return Game.progress.toys.filter(Boolean).length; },
  unlocked(c) { return this.toys() >= c.toys; },
  equipped(c) {
    const E = Game.progress.cosmetics;
    return c.kind === 'fur' ? E.fur === c.id : !!E[c.kind];
  },
  choose(c) {
    if (!this.unlocked(c)) { UI.toast(`FIND ${c.toys} TOYS TO UNLOCK`); return; }
    const E = Game.progress.cosmetics;
    if (c.kind === 'fur') E.fur = c.id; else E[c.kind] = !E[c.kind];
    Game.saveProgress();
    this.apply();
    UI.refreshSettings();
  },
  init() {
    // bell bracelet on the right wrist (silent: it is only for looks)
    const gold = PropMat.lambert(0xc8a040, 'braceletGold');
    const parts = [[new THREE.TorusGeometry(0.038, 0.007, 6, 16), 0, -0.005, 0.07, Math.PI / 2]];
    for (let i = 0; i < 4; i++) { const a = i / 4 * Math.PI * 2; parts.push([new THREE.SphereGeometry(0.011, 6, 4), Math.cos(a) * 0.04, -0.005 + Math.sin(a) * 0.04, 0.07]); }
    this.bracelet = mergeInto(Player.hands[1].visual, gold, parts);
    // lantern-shaped flashlight on the left hand
    const lp = [[new THREE.BoxGeometry(0.045, 0.06, 0.045), 0, 0.055, 0.03], [new THREE.ConeGeometry(0.035, 0.025, 4), 0, 0.097, 0.03, 0, Math.PI / 4], [new THREE.TorusGeometry(0.012, 0.003, 4, 8), 0, 0.115, 0.03]];
    this.lanternModel = mergeInto(Player.hands[0].visual, PropMat.lambert(0x2a2622, 'lanternMetal'), lp);
    this.lanternGlow = propMesh(new THREE.BoxGeometry(0.03, 0.04, 0.03), PropMat.basic(0xffc060, 'flame'), Player.hands[0].visual, 0, 0.055, 0.03);
    this.apply();
  },
  apply() {
    const E = Game.progress.cosmetics;
    const fur = COSMETICS.find((c) => c.id === E.fur) || COSMETICS[0];
    for (const h of Player.hands) {
      h.visual.traverse((o) => {
        if (o.isMesh && o.material && o.material.map && TEX_CACHE.get('hair') && (o.material.userData.handFur || o.material.map === TEX_CACHE.get('hair'))) {
          o.material.userData.handFur = true;
          o.material.map = getTexture(fur.tex);
          o.material.color.setScalar(fur.id === 'fur_default' ? 1 : 1.9);
        }
      });
    }
    if (this.bracelet) this.bracelet.visible = !!E.bracelet;
    if (this.lanternModel) { this.lanternModel.visible = !!E.lantern; this.lanternGlow.visible = !!E.lantern; }
    Flashlight.light.color.setHex(E.lantern ? 0xffc27a : 0xfff1d6);
    Hub.refreshShelf();
  },
};

// --------------------------------------------------------------- Throwables and flares (a separate grabbable layer)
const PROP_DEFS = {
  bottle: { r: 0.045, max: 14, lie: true },
  can: { r: 0.04, max: 14, lie: true },
  stone: { r: 0.05, max: 18, lie: false },
  flare: { r: 0.03, max: 6, lie: true },
};
const FLARE_COLD = new THREE.Color(0.55, 0.08, 0.06), FLARE_LIT = new THREE.Color(1.0, 0.45, 0.3), FLARE_BURNT = new THREE.Color(0.14, 0.11, 0.1);
class Prop {
  constructor(type, p) {
    this.type = type; this.r = PROP_DEFS[type].r;
    this.pos = new THREE.Vector3().fromArray(p); this.home = this.pos.clone();
    this.vel = new THREE.Vector3(); this.spin = new THREE.Vector3(); this.quat = new THREE.Quaternion();
    this.held = null; this.asleep = true; this.sleepT = 0; this.broken = false; this.thrown = false; this.noiseT = 0; this.contact = false;
    this.lit = false; this.litT = 0; this.burnt = false; this.shakes = 0; this.shakeArmed = true; this.lastShakeT = -99; this.lureT = 0;
  }
}
const Grab = {
  props: [], meshes: {}, counts: { bottle: 0, can: 0, stone: 0, flare: 0 }, flareLight: null, litFlare: null, glow: null,
  hist: [[], []], histIdx: 0,
  _filter: (c) => !c.noProps,
  build(scene) {
    const bottle = new THREE.LatheGeometry([[0, 0], [0.04, 0], [0.045, 0.02], [0.045, 0.13], [0.03, 0.17], [0.014, 0.19], [0.014, 0.235], [0.017, 0.24], [0, 0.24]].map(([x, y]) => new THREE.Vector2(x, y)), 10);
    bottle.translate(0, -0.12, 0);
    const can = colorizeGeometry(new THREE.CylinderGeometry(0.033, 0.033, 0.12, 10), 0x9a8a78, 0.15);
    const stone = new THREE.IcosahedronGeometry(0.055, 0); stone.scale(1, 0.72, 1.2);
    const fp = [colorizeGeometry(new THREE.CylinderGeometry(0.022, 0.022, 0.2, 8), 0xffffff, 0), colorizeGeometry(new THREE.CylinderGeometry(0.025, 0.025, 0.035, 8), 0x303030, 0)];
    fp[1].translate(0, 0.1, 0);
    const flare = mergeGeometries(fp); fp.forEach((g) => g.dispose());
    const mats = {
      bottle: new THREE.MeshLambertMaterial({ color: 0x3a6a40, emissive: 0x081208 }),
      can: new THREE.MeshLambertMaterial({ map: getTexture('metal'), vertexColors: true }),
      stone: new THREE.MeshLambertMaterial({ color: 0x9a9488, flatShading: true }),
      flare: new THREE.MeshBasicMaterial({ vertexColors: true }),
    };
    const geos = { bottle, can, stone, flare };
    for (const t in PROP_DEFS) {
      mats[t].userData.shared = true;
      const im = new THREE.InstancedMesh(geos[t], mats[t], PROP_DEFS[t].max);
      im.count = 0; im.frustumCulled = false; im.instanceMatrix.setUsage(THREE.DynamicDrawUsage);
      if (t === 'flare') for (let i = 0; i < PROP_DEFS[t].max; i++) im.setColorAt(i, FLARE_COLD);
      scene.add(im); this.meshes[t] = im;
    }
    // a burning flare's glare (one additive sprite)
    const c = makeCanvas(64, 64), ctx = c.getContext('2d');
    const gr = ctx.createRadialGradient(32, 32, 0, 32, 32, 32);
    gr.addColorStop(0, 'rgba(255,220,180,1)'); gr.addColorStop(0.25, 'rgba(255,80,40,0.8)'); gr.addColorStop(1, 'rgba(255,0,0,0)');
    ctx.fillStyle = gr; ctx.fillRect(0, 0, 64, 64);
    const tex = new THREE.CanvasTexture(c); tex.colorSpace = THREE.SRGBColorSpace;
    this.glow = new THREE.Sprite(new THREE.SpriteMaterial({ map: tex, blending: THREE.AdditiveBlending, depthWrite: false, transparent: true }));
    this.glow.visible = false; scene.add(this.glow);
    for (let s = 0; s < 2; s++) for (let i = 0; i < 6; i++) this.hist[s].push({ p: new THREE.Vector3(), t: -1 });
  },
  clear() {
    for (const h of Player.hands) h.holding = null;
    this.props.length = 0; this.litFlare = null; this.flareLight = null;
    this.glow.visible = false;
    AudioSys.setFlareLoop(0, null);
    this.render();
  },
  setupLevel(data) {
    this.clear();
    for (const d of data.props || []) {
      if (this.props.length >= 48) break;
      const p = new Prop(d.type, d.p);
      p.quat.setFromAxisAngle(UP, Math.random() * Math.PI * 2);
      this.settle(p);
      this.props.push(p);
    }
    // a red light only in levels that have flares (the light count must not change mid-level)
    if (this.props.some((p) => p.type === 'flare')) {
      this.flareLight = new THREE.PointLight(0xff3a20, 0, U1.FLARE_DISTANCE, 1.5);
      Level.root.add(this.flareLight);
    }
    this.render();
  },
  settle(p) {
    _gv.copy(p.pos); _gv.y += 0.3;
    if (World.raycast(_gv, DOWN, 3, this._filter, _gHit)) p.pos.y = _gv.y - _gHit.t + p.r;
    if (PROP_DEFS[p.type].lie) p.quat.setFromEuler(_gE.set(Math.PI / 2, 0, Math.random() * Math.PI * 2));
    p.asleep = true; p.vel.set(0, 0, 0); p.spin.set(0, 0, 0);
  },
  resetForRespawn() {   // things in your hands drop where you were caught
    for (const h of Player.hands) if (h.holding) this.drop(h);
  },
  nearestLitFlare(pos, r) { const f = this.litFlare; return f && f.pos.distanceTo(pos) < r ? f : null; },

  update(dt) {
    // world-space hand history (throws use the averaged velocity of the last frames)
    this.histIdx = (this.histIdx + 1) % 6;
    for (let s = 0; s < 2; s++) { const e = this.hist[s][this.histIdx]; e.p.copy(Player.hands[s].phys); e.t = Game.time; }
    for (const h of Player.hands) this.updateHand(h);
    for (const p of this.props) if (!p.held && !p.asleep && !p.broken) this.simulate(p, dt);
    this.updateFlares(dt);
    this.render();
  },
  handVelocity(side, out) {
    const H = this.hist[side], newest = H[this.histIdx], oldest = H[(this.histIdx + 1) % 6];
    const dt = newest.t - oldest.t;
    if (oldest.t < 0 || dt <= 1e-4) return out.set(0, 0, 0);
    return out.copy(newest.p).sub(oldest.p).multiplyScalar(1 / dt);
  },
  updateHand(h) {
    const toggle = Game.progress.settings.gripMode === 'toggle';
    const pressed = h.squeeze > 0.6 && !h.gripWas;
    const released = h.squeeze < 0.35 && h.gripWas;
    if (h.squeeze > 0.6) h.gripWas = true; else if (h.squeeze < 0.35) h.gripWas = false;
    const active = Game.state === 'PLAYING' || Game.state === 'MENU';
    if (h.cord) { if ((toggle ? pressed : released) || !active) Cords.letGo(h.cord); return; }
    if (h.holding) {
      const p = h.holding;
      p.pos.copy(h.phys).add(_gv.set(0, -0.01, -0.07).applyQuaternion(h.worldQuat));   // in the palm
      p.quat.copy(h.worldQuat);
      if (p.type === 'flare') this.flareShake(p, h);
      if ((toggle ? pressed : released) || !active) this.throwProp(h);
      return;
    }
    if (!active || !pressed || h.cling) return;
    if (Cords.tryGrab(h)) return;   // cords first (The Heart)
    let best = null, bd = 1e9;
    const reach = U1.GRAB_RADIUS + (Input.xr ? 0 : 0.14);
    for (const p of this.props) {
      if (p.held || p.broken) continue;
      const d = p.pos.distanceTo(h.phys) - p.r;
      if (d < reach && d < bd) { bd = d; best = p; }
    }
    if (best) this.pickUp(h, best);
  },
  pickUp(h, p) {
    if (h.anchored) Player.release(h, false);   // a hand holding a prop cannot anchor
    h.holding = p; p.held = h; p.asleep = false; p.thrown = false;
    AudioSys.click(0.15); Input.haptic(h.side, 0.3, 30);
    if (p.type === 'flare' && !p.lit && !p.burnt) Game.toast(Input.xr ? 'SHAKE IT TO STRIKE THE FLARE' : 'PRESS X TO SHAKE THE FLARE');
  },
  drop(h) {
    const p = h.holding;
    if (!p) return;
    h.holding = null; p.held = null; p.asleep = false; p.sleepT = 0; p.thrown = false; p.vel.set(0, 0, 0);
  },
  throwProp(h) {
    const p = h.holding;
    if (!p) return;
    h.holding = null; p.held = null; p.asleep = false; p.sleepT = 0; p.thrown = true; p.noiseT = 0;
    h.cooldown = Math.max(h.cooldown, 0.12);
    if (Input.desktopActive && !Input.xr) p.vel.set(0, 0, -7).applyQuaternion(Player.headWorldQuat).add(_gw.set(0, 2, 0));
    else {
      this.handVelocity(h.side, p.vel).multiplyScalar(U1.THROW_MULTIPLIER);
      const sp = p.vel.length();
      if (sp > U1.THROW_MAX_SPEED) p.vel.multiplyScalar(U1.THROW_MAX_SPEED / sp);
    }
    const sp = p.vel.length();
    p.spin.set(Math.random() - 0.5, Math.random() - 0.5, Math.random() - 0.5).multiplyScalar(sp * 3);
    if (sp > 3) AudioSys.whoosh(p.pos, Math.min(0.4, sp / 30));
  },
  simulate(p, dt) {
    const water = Water.active && p.pos.y < Water.level;
    const g = water ? (p.type === 'stone' ? 0.6 : -0.8) : 1;   // bottles, cans and flares float
    const steps = clamp(Math.ceil(p.vel.length() * dt / (p.r * 1.5)), 1, 6), h = dt / steps;
    p.contact = false;
    for (let s = 0; s < steps; s++) {
      p.vel.y += CONFIG.GRAVITY * h * g;
      p.pos.addScaledVector(p.vel, h);
      if (!World.resolveSphere(p.pos, p.r, _gp, null, this._filter, 3)) continue;
      p.pos.add(_gp);
      _gn.copy(_gp).normalize();
      const vn = p.vel.dot(_gn);
      if (vn >= 0) continue;
      p.contact = true;
      const impact = -vn;
      p.vel.addScaledVector(_gn, -vn * (1 + U1.PROP_RESTITUTION));
      _gt.copy(p.vel).addScaledVector(_gn, -p.vel.dot(_gn));
      if (impact > 0.5) p.vel.addScaledVector(_gt, -(1 - U1.PROP_FRICTION));
      if (impact > U1.PROP_NOISE_MIN_SPEED) this.impact(p, impact);
      if (p.broken) return;
    }
    if (water) p.vel.multiplyScalar(Math.exp(-3 * dt));
    if (p.contact) {
      // rolling: round things keep rolling a while, stones scrape to a stop
      const keep = p.type === 'stone' ? 0.9 : 0.985;
      const f = Math.pow(keep, dt * 60);
      p.vel.x *= f; p.vel.z *= f;
      _gt.set(p.vel.z, 0, -p.vel.x).multiplyScalar(1 / p.r);
      p.spin.lerp(_gt, 0.3);
    }
    if (p.spin.lengthSq() > 1e-6) {
      const w = p.spin.length();
      p.quat.premultiply(_gq.setFromAxisAngle(_gt.copy(p.spin).multiplyScalar(1 / w), w * dt));
      p.spin.multiplyScalar(p.contact ? 0.97 : 0.995);
    }
    if (p.vel.lengthSq() < 0.0025 && (p.contact || water)) {
      p.sleepT += dt;
      if (p.sleepT > 0.5 && !water) { this.settle(p); p.thrown = false; }
    } else p.sleepT = 0;
    const killY = Level.data && Level.data.killY !== undefined ? Level.data.killY : -40;
    if (p.pos.y < killY) { p.pos.copy(p.home); this.settle(p); }
  },
  impact(p, speed) {
    if (Game.time - p.noiseT < 0.12) return;
    p.noiseT = Game.time;
    const loud = U1.PROP_NOISE[p.type] * clamp(speed / 6, 0.35, 1.3);
    if (p.type === 'bottle' && speed > U1.BOTTLE_SHATTER_SPEED) {
      p.broken = true; p.asleep = true;
      AudioSys.shatter(p.pos, 1);
      Dust.emit(p.pos, 18, 0.3, 0x90c0a0, 1.2, 1.2, 1.6);   // a little burst of glass
      Subtitles.add('[glass shatters]', p.pos);
      this.makeNoise(p, loud * 1.3);
      return;
    }
    if (p.type === 'stone') AudioSys.impact('DEFAULT', p.pos, speed);
    else AudioSys.tink(p.pos, clamp(speed / 6, 0.2, 0.8), p.type === 'can' ? 700 : 1500);
    if (p.thrown) this.makeNoise(p, loud);
  },
  makeNoise(p, loud) {
    const lured = Game.noise(p.pos, loud, 'prop');
    if (lured && p.thrown) Achievements.award('bait');
  },
  // ---------- flares
  flareShake(p, h) {
    if (p.lit || p.burnt) return;
    const sp = Input.xr || !Input.desktopActive ? h.relVel.length() : (Input.shakePulse ? 99 : 0);
    if (sp > U1.CRAWLER_SHAKE_SPEED && p.shakeArmed) {
      p.shakeArmed = false; p.shakes++; p.lastShakeT = Game.time;
      AudioSys.click(0.1); Input.haptic(h.side, 0.4, 30);
      if (p.shakes >= U1.FLARE_SHAKES) this.ignite(p);
    } else if (sp < U1.CRAWLER_SHAKE_SPEED * 0.5) p.shakeArmed = true;
    if (Game.time - p.lastShakeT > 1.5) p.shakes = 0;
  },
  ignite(p) {
    p.lit = true; p.litT = U1.FLARE_TIME; p.lureT = 0.6;
    AudioSys.flareIgnite(p.pos);
    Input.hapticBoth(0.4, 120);
    Game.toast('FLARE LIT');
    Subtitles.add('[a flare hisses]', p.pos);
  },
  updateFlares(dt) {
    let best = null;
    for (const p of this.props) {
      if (!p.lit) continue;
      p.litT -= dt;
      if (p.litT <= 0) { p.lit = false; p.burnt = true; continue; }
      if (!best || p.litT > best.litT) best = p;
      p.lureT -= dt;
      if (p.lureT <= 0 && Game.state === 'PLAYING') {   // the Warden comes to look at the light
        p.lureT = U1.FLARE_LURE_INTERVAL;
        const lured = Game.noise(p.pos, U1.FLARE_LURE_LOUDNESS, 'flare');
        if (lured && !p.held) Achievements.award('bait');
      }
      if (Math.random() < dt * 25) Dust.emit(p.pos, 1, 0.02, 0xff6030, 0.4 + Math.random(), 0.6, 0.5);   // sparks
    }
    this.litFlare = best;
    const flick = 0.8 + Math.random() * 0.25;
    if (this.flareLight) {
      if (best) { this.flareLight.position.copy(best.pos); this.flareLight.position.y += 0.15; }
      this.flareLight.intensity = best ? U1.FLARE_INTENSITY * CONFIG.LIGHT_SCALE * flick * Math.min(1, best.litT / 2) : 0;
    }
    this.glow.visible = !!best;
    if (best) { this.glow.position.copy(best.pos); const s = 0.35 * flick; this.glow.scale.set(s, s, s); }
    AudioSys.setFlareLoop(best ? 0.25 : 0, best ? best.pos : null);
  },
  render() {
    const C = this.counts;
    C.bottle = C.can = C.stone = C.flare = 0;
    for (const p of this.props) {
      if (p.broken) continue;
      const im = this.meshes[p.type], i = C[p.type]++;
      im.setMatrixAt(i, _gm.compose(p.pos, p.quat, ONE3));
      if (p.type === 'flare') im.setColorAt(i, p.lit ? FLARE_LIT : p.burnt ? FLARE_BURNT : FLARE_COLD);
    }
    for (const t in this.meshes) {
      const im = this.meshes[t];
      im.count = C[t];
      if (C[t]) { im.instanceMatrix.needsUpdate = true; if (im.instanceColor) im.instanceColor.needsUpdate = true; }
    }
  },
};
const _gHit = { t: 0, collider: null };
const _gE = new THREE.Euler();

// --------------------------------------------------------------- Hiding spots: lockers, wardrobes, barrels, crawlspaces, flesh pods
const HIDE_TYPES = {
  locker: { w: 0.8, h: 2.0, d: 0.8, mat: 'metal', color: 0x5a6a60, round: false },
  wardrobe: { w: 1.6, h: 2.2, d: 0.95, mat: 'wood', color: 0x6a4a30, round: false, backHole: true },
  barrel: { r: 0.55, h: 1.15, mat: 'wood', color: 0x7a5a3a, round: true },
  pod: { r: 0.72, h: 1.5, mat: 'flesh', color: 0xb05a5a, round: true },
  crawlspace: { w: 2.6, h: 1.0, d: 1.6, mat: 'wood', color: 0x5a4430, round: false, low: true },
};
class HidingSpot extends Interactable {
  constructor(def) {
    super();
    const T = this.T = HIDE_TYPES[def.type] || HIDE_TYPES.locker;
    this.type = def.type;
    this.pos = new THREE.Vector3().fromArray(def.p);
    this.q = new THREE.Quaternion().setFromAxisAngle(UP, (def.yaw || 0) * DEG);
    this.invQ = this.q.clone().invert();
    const g = this.group; g.position.copy(this.pos); g.quaternion.copy(this.q);
    this.door = new THREE.Group(); g.add(this.door);
    this.anim = 0; this.isOpen = false; this.holdOpen = false; this.insideT = 0; this.wardenK = -1; this.wasInside = false;
    this.center = this.local(0, (T.h || 1) * 0.5, 0, new THREE.Vector3());
    const geos = [], doorGeos = [], th = 0.05;
    const wall = (x, y, z, sx, sy, sz, list = geos, collide = true) => {
      const geo = colorizeGeometry(new THREE.BoxGeometry(sx, sy, sz), T.color, 0.1);
      geo.translate(x, y, z); list.push(geo);
      if (!collide) return null;
      const c = World.makeBox(this.local(x, y, z, _iv), this.q, _iw.set(sx / 2, sy / 2, sz / 2), T.mat === 'flesh' ? 'STICKY' : 'DEFAULT');
      return addCollider(this, c);
    };
    if (T.round) {
      const N = 10, R = T.r;
      for (let i = 0; i < N; i++) {
        const a = i / N * Math.PI * 2, segW = 2 * Math.PI * R / N * 1.08;
        const geo = colorizeGeometry(new THREE.BoxGeometry(segW, T.h, th * 1.6), T.color, 0.12);
        geo.rotateY(-a + Math.PI / 2); geo.translate(Math.cos(a) * R, T.h / 2, Math.sin(a) * R); geos.push(geo);
        addCollider(this, World.makeBox(this.local(Math.cos(a) * R, T.h / 2, Math.sin(a) * R, _iv), _q2.copy(this.q).multiply(_q3.setFromAxisAngle(UP, -a + Math.PI / 2)), _iw.set(segW / 2, T.h / 2, th * 0.8)));
      }
      if (T.mat !== 'flesh') for (const y of [0.2, T.h - 0.2]) { const band = colorizeGeometry(new THREE.TorusGeometry(R + 0.04, 0.025, 4, 18), 0x3a3632); band.rotateX(Math.PI / 2); band.translate(0, y, 0); geos.push(band); }
      wall(0, th / 2, 0, R * 1.6, th, R * 1.6);
      // the lid slides off the top
      const lid = colorizeGeometry(new THREE.CylinderGeometry(R + 0.03, R + 0.03, 0.07, 14), T.color, 0.1);
      doorGeos.push(lid);
      this.door.position.set(0, T.h + 0.035, 0);
      this.doorCol = addCollider(this, World.makeCyl(this.local(0, T.h + 0.035, 0, _iv), this.q, R + 0.03, 0.035));
      this.handleL = new THREE.Vector3(R * 0.7, T.h + 0.08, 0);
      this.inner = { r: R - th, y0: 0, y1: T.h };
    } else if (T.low) {
      // crawlspace: a low deck with a hatch on top; the far end is open (your second way out)
      const { w, h, d } = T, hx0 = -1.05, hx1 = -0.15;
      wall((-w / 2 + hx0) / 2, h - 0.05, 0, hx0 + w / 2, 0.1, d);
      wall((hx1 + w / 2) / 2, h - 0.05, 0, w / 2 - hx1, 0.1, d);
      wall((hx0 + hx1) / 2, h - 0.05, (0.45 + d / 2) / 2, hx1 - hx0, 0.1, d / 2 - 0.45);
      wall((hx0 + hx1) / 2, h - 0.05, -(0.45 + d / 2) / 2, hx1 - hx0, 0.1, d / 2 - 0.45);
      wall(0, (h - 0.1) / 2, -d / 2 + th / 2, w, h - 0.1, th);
      wall(0, (h - 0.1) / 2, d / 2 - th / 2, w, h - 0.1, th);
      wall(-w / 2 + th / 2, (h - 0.1) / 2, 0, th, h - 0.1, d);
      for (const x of [-w / 2 + 0.3, 0, w / 2 - 0.3]) wall(x, h - 0.15, 0, 0.12, 0.1, d, geos, false);   // joists
      const hatch = colorizeGeometry(new THREE.BoxGeometry(hx1 - hx0, 0.08, 0.9), 0x4a3828, 0.1);
      hatch.translate((hx1 - hx0) / 2, 0, 0); doorGeos.push(hatch);
      this.door.position.set(hx0, h - 0.04, 0);
      this.doorCol = addCollider(this, World.makeBox(this.local((hx0 + hx1) / 2, h - 0.04, 0, _iv), this.q, _iw.set((hx1 - hx0) / 2, 0.04, 0.45)));
      this.handleL = new THREE.Vector3(hx1 - 0.05, h + 0.05, 0);
      this.inner = { x0: -w / 2 + th, x1: w / 2, y0: 0, y1: h - 0.1, z0: -d / 2 + th, z1: d / 2 - th };
    } else {
      // locker / wardrobe: a box with a hinged door on the +Z face
      const { w, h, d } = T;
      if (T.backHole) {   // a rotten hole low in the back: squeeze out the other side
        const hw = 0.42, hh = 0.8;
        wall((-w / 2 - hw) / 2, h / 2, -d / 2 + th / 2, w / 2 - hw, h, th);
        wall((w / 2 + hw) / 2, h / 2, -d / 2 + th / 2, w / 2 - hw, h, th);
        wall(0, (hh + h) / 2, -d / 2 + th / 2, hw * 2, h - hh, th);
      } else wall(0, h / 2, -d / 2 + th / 2, w, h, th);
      wall(-w / 2 + th / 2, h / 2, 0, th, h, d);
      wall(w / 2 - th / 2, h / 2, 0, th, h, d);
      wall(0, h - th / 2, 0, w, th, d);
      wall(0, th / 2, 0, w, th, d);
      const panel = colorizeGeometry(new THREE.BoxGeometry(w, h - 0.02, th), T.color, 0.08);
      panel.translate(w / 2, h / 2, 0); doorGeos.push(panel);
      if (this.type === 'locker') for (let k = 0; k < 6; k++) { const slat = colorizeGeometry(new THREE.BoxGeometry(w * 0.6, 0.03, 0.012), 0x101410, 0.02); slat.translate(w / 2, h * 0.7 + k * 0.06, th / 2 + 0.004); doorGeos.push(slat); }
      else { const knob = colorizeGeometry(new THREE.SphereGeometry(0.03, 6, 4), 0xa08040); knob.translate(w - 0.1, h * 0.5, th); doorGeos.push(knob); }
      this.door.position.set(-w / 2, 0, d / 2 - th / 2);
      this.doorCol = addCollider(this, World.makeBox(this.local(0, h / 2, d / 2 - th / 2, _iv), this.q, _iw.set(w / 2, h / 2, th / 2)));
      this.handleL = new THREE.Vector3(w / 2 - 0.08, h * 0.55, d / 2 + 0.05);
      this.inner = { x0: -w / 2 + th, x1: w / 2 - th, y0: 0, y1: h - th, z0: -d / 2 + th, z1: d / 2 - th };
    }
    const mat = getMaterial(T.mat);
    const body = mergeGeometries(geos); geos.forEach((x) => x.dispose()); worldUV(body, 1.5);
    g.add(new THREE.Mesh(body, mat));
    const dg = mergeGeometries(doorGeos); doorGeos.forEach((x) => x.dispose()); worldUV(dg, 1.5);
    this.door.add(new THREE.Mesh(dg, mat));
    this.handle = this.local(this.handleL.x, this.handleL.y, this.handleL.z, new THREE.Vector3());
    this.front = this.local(0, 0, (T.d || T.r * 2) / 2 + 2.8, new THREE.Vector3());
    this.front.y = this.pos.y;
  }
  local(x, y, z, out) { return out.set(x, y, z).applyQuaternion(this.q).add(this.pos); }
  contains(p) {
    const L = _gv.copy(p).sub(this.pos).applyQuaternion(this.invQ), I = this.inner;
    if (this.T.round) return L.y > I.y0 && L.y < I.y1 && L.x * L.x + L.z * L.z < I.r * I.r;
    return L.x > I.x0 && L.x < I.x1 && L.y > I.y0 && L.y < I.y1 && L.z > I.z0 && L.z < I.z1;
  }
  onTouch(h, speed) { if (speed > 0.35) this.open(this.contains(Player.head)); }   // a deliberate push, not a door closing onto a resting hand
  open(fromInside) {
    if (this.isOpen) return;
    this.isOpen = true; this.holdOpen = !!fromInside;
    AudioSys.lidCreak(this.handle, 0.4);
    Game.noise(this.handle, 1.0, 'hide');
  }
  forceOpen() { if (!this.isOpen) AudioSys.crash(this.handle, 0.4); this.isOpen = true; this.holdOpen = true; this.wardenK = -1; this.fast = true; }
  wardenOpen(k) {
    if (this.wardenK < 0) { AudioSys.lidCreak(this.handle, 0.6); Subtitles.add('[a door creaks open]', this.handle); }
    this.wardenK = k;
  }
  wardenRelease() { if (this.wardenK >= 0) { this.wardenK = -1; this.isOpen = true; this.holdOpen = true; } }
  update(dt) {
    const inside = this.contains(Player.head);
    this.insideT = inside ? this.insideT + dt : 0;
    if (!inside && this.wasInside) this.holdOpen = false;   // you left: it may close behind the next one in
    this.wasInside = inside;
    // pulled shut behind you once you are in
    if (this.isOpen && inside && !this.holdOpen && this.wardenK < 0 && this.insideT > U1.HIDE_ENTER_TIME && Game.state === 'PLAYING') {
      this.isOpen = false;
      AudioSys.lidCreak(this.handle, 0.25);
    }
    const target = this.wardenK >= 0 ? this.wardenK : this.isOpen ? 1 : 0;
    const speed = this.wardenK >= 0 ? 4 : this.fast ? 6 : 2.5;
    this.anim = target > this.anim ? Math.min(target, this.anim + dt * speed) : Math.max(target, this.anim - dt * speed);
    if (this.anim === target) this.fast = false;
    const a = this.anim;
    if (this.T.round) { this.door.position.x = a * (this.T.r + 0.35); this.door.position.y = this.T.h + 0.035 + Math.sin(a * Math.PI) * 0.15; this.door.rotation.z = -a * 0.5; }
    else if (this.T.low) this.door.rotation.z = a * 1.9;
    else this.door.rotation.y = -a * 1.9;
    this.doorCol.enabled = a < 0.35;
  }
}
const Hiding = {
  spots: [], current: null, seenEnter: false, overlay: null, overlayK: 0, noiseT: 0, breathT: 0,
  init(camera) {
    const c = makeCanvas(256, 256), ctx = c.getContext('2d');
    ctx.fillStyle = 'rgba(0,0,0,0.94)'; ctx.fillRect(0, 0, 256, 256);
    for (let y = 30; y < 256; y += 38) {   // thin slats of light through the door
      const g = ctx.createLinearGradient(0, y - 6, 0, y + 6);
      g.addColorStop(0, 'rgba(0,0,0,0.94)'); g.addColorStop(0.5, 'rgba(255,220,170,0.08)'); g.addColorStop(1, 'rgba(0,0,0,0.94)');
      ctx.clearRect(0, y - 6, 256, 12); ctx.fillStyle = g; ctx.fillRect(0, y - 6, 256, 12);
    }
    const tex = new THREE.CanvasTexture(c); tex.colorSpace = THREE.SRGBColorSpace;
    this.overlay = new THREE.Mesh(new THREE.PlaneGeometry(0.7, 0.7), new THREE.MeshBasicMaterial({ map: tex, transparent: true, opacity: 0, depthTest: false, depthWrite: false, fog: false }));
    this.overlay.position.z = -0.14; this.overlay.renderOrder = 998; this.overlay.frustumCulled = false; this.overlay.visible = false;
    camera.add(this.overlay);
  },
  clear() { this.spots.length = 0; this.current = null; this.seenEnter = false; this.breathT = 0; },
  add(def) { const s = new HidingSpot(def); this.spots.push(s); return Interact.add(s); },
  spotToCheck(from, checked) {
    if (checked.size >= 2) return null;
    let best = null, bd = U1.HIDE_CHECK_RADIUS;
    for (const s of this.spots) { const d = s.center.distanceTo(from); if (d < bd && !checked.has(s)) { bd = d; best = s; } }
    return best;
  },
  forceOpen() { if (this.current) this.current.forceOpen(); },
  update(dt) {
    let cur = null;
    for (const s of this.spots) if (s.anim < 0.3 && s.contains(Player.head)) { cur = s; break; }
    if (cur !== this.current) {
      if (cur) {
        this.seenEnter = Warden.active && (Warden.seesPlayer || Game.time - Warden.lastSeenT < 1.2);
        Subtitles.add('[you hold your breath]', null);
      }
      this.current = cur; this.breathT = 0;
    }
    this.overlayK = damp(this.overlayK, cur ? 1 : 0, 6, dt);
    this.overlay.material.opacity = this.overlayK;
    this.overlay.visible = this.overlayK > 0.01;
    this.overlay.rotation.z = cur && cur.type === 'wardrobe' ? Math.PI / 2 : 0;
    if (!cur || Game.state !== 'PLAYING') return;
    // hold still: moving your hands inside makes noise
    this.noiseT -= dt;
    for (const h of Player.hands) {
      if (this.noiseT > 0) break;
      if (h.relVel.length() > U1.HIDE_MOVE_NOISE_SPEED) {
        this.noiseT = 0.4;
        Game.noise(h.phys, U1.HIDE_MOVE_NOISE, 'hide');
        AudioSys.impact(cur.T.mat === 'metal' ? 'NOISY' : 'DEFAULT', h.phys, 0.5);
        Input.haptic(h.side, 0.2, 20);
      }
    }
    if (Warden.active && Warden.root.visible && Math.hypot(Warden.pos.x - Player.head.x, Warden.pos.z - Player.head.z) < U1.HELD_BREATH_RANGE) {
      this.breathT += dt;
      if (this.breathT > U1.HELD_BREATH_TIME) Achievements.award('heldbreath');
    } else this.breathT = 0;
  },
};

// --------------------------------------------------------------- Rising water (The Flooded Chapel)
let WATER_TEX = null;
const Water = {
  active: false, level: -1e9, target: -1e9, max: 0, timer: 0, final: false, mesh: null, mat: null, cfg: null,
  drownT: 0, headUnder: false, muffle: 0, wetSurf: {}, fogSaved: false, savedFogColor: new THREE.Color(), savedFogDensity: 0, tint: null,
  init(camera) {
    const SL = CONFIG.SURFACES.SLIPPERY;
    for (const k in CONFIG.SURFACES) {
      const s = CONFIG.SURFACES[k];
      this.wetSurf[k] = Object.assign({}, s, { bodyGrip: Math.min(s.bodyGrip, SL.bodyGrip), handGrip: Math.min(s.handGrip, SL.handGrip) });
    }
    WATER_TEX = getTexture('water').clone(); WATER_TEX.needsUpdate = true; WATER_TEX.userData.shared = true;
    this.mat = new THREE.MeshLambertMaterial({ map: WATER_TEX, color: 0x507068, transparent: true, opacity: 0.78, depthWrite: false, side: THREE.DoubleSide });
    this.mat.userData.shared = true;
    this.tint = new THREE.Mesh(new THREE.PlaneGeometry(0.7, 0.7), new THREE.MeshBasicMaterial({ color: 0x0a3a34, transparent: true, opacity: 0, depthTest: false, depthWrite: false, fog: false }));
    this.tint.position.z = -0.13; this.tint.renderOrder = 997; this.tint.visible = false; this.tint.frustumCulled = false;
    camera.add(this.tint);
  },
  surface(key) { return this.wetSurf[key] || this.wetSurf.DEFAULT; },
  setupLevel(data) {
    const w = data.water;
    this.cfg = w || null; this.active = !!w; this.drownT = 0; this.fogSaved = false; this.headUnder = false; this.muffle = 0;
    this.tint.visible = false; this.tint.material.opacity = 0;
    if (!w) { this.level = this.target = -1e9; this.mesh = null; AudioSys.setRush(0); return; }
    this.level = this.target = w.level; this.max = w.max; this.final = false;
    this.timer = U1.WATER_RISE_INTERVAL;
    const [x0, z0, x1, z1] = w.area;
    const geo = new THREE.PlaneGeometry(x1 - x0, z1 - z0, 1, 1); geo.rotateX(-Math.PI / 2);
    const uv = geo.attributes.uv; for (let i = 0; i < uv.count; i++) uv.setXY(i, uv.getX(i) * (x1 - x0) / 5, uv.getY(i) * (z1 - z0) / 5);
    this.mesh = new THREE.Mesh(geo, this.mat);
    this.mesh.position.set((x0 + x1) / 2, this.level, (z0 + z1) / 2); this.mesh.renderOrder = 2;
    Level.root.add(this.mesh);
  },
  snapshot(o) { o.level = this.target; o.timer = this.timer; o.final = this.final; o.max = this.max; return o; },
  restore(o) {
    if (!this.active || o.level === undefined) return;
    this.level = this.target = o.level; this.timer = Math.max(o.timer, 20); this.final = o.final; this.max = o.max;
  },
  startFinal() { this.final = true; this.max = this.cfg.finalMax; this.timer = 3; },
  debugRaise() {
    if (!this.active) { Game.toast('NO WATER IN THIS LEVEL'); return; }
    this.target = Math.min(this.max, this.target + U1.WATER_RISE_STEP); this.level = this.target; this.timer = U1.WATER_RISE_INTERVAL;
    Game.toast(`WATER ${this.level.toFixed(1)} m`);
  },
  splash(p, strength) {   // the Warden wading
    _gv.set(p.x, this.level + 0.05, p.z);
    AudioSys.bigSplash(_gv, clamp(strength * 0.7, 0.3, 1));
    Dust.emit(_gv, 14, 1.4, 0xd8e8e8, 1.6, 1.2, 1.4);
    Subtitles.add('[splashing]', _gv, 'splash');
  },
  update(dt) {
    if (!this.active) { this.muffle = 0; return; }
    if (Game.state === 'PLAYING') {
      this.timer -= dt;
      if (this.timer <= 0) {
        if (this.target < this.max - 1e-3) {
          this.target = Math.min(this.max, this.target + U1.WATER_RISE_STEP);
          Game.toast('THE WATER IS RISING');
          Subtitles.add('[rushing water]', null);
          Input.hapticBoth(0.3, 400);
          AudioSys.thud(Player.head, 0.3);
        }
        this.timer = this.final ? U1.WATER_RISE_INTERVAL_FINAL : U1.WATER_RISE_INTERVAL;
      }
    }
    const rising = this.level < this.target - 0.005;
    if (rising) this.level = Math.min(this.target, this.level + dt * U1.WATER_RISE_STEP / U1.WATER_RISE_TIME);
    AudioSys.setRush(rising ? 1 : 0.12);
    this.mesh.position.y = this.level;
    WATER_TEX.offset.x += dt * 0.012; WATER_TEX.offset.y += dt * 0.007;
    // your hands breaking the surface
    for (const h of Player.hands) {
      const under = h.phys.y < this.level;
      if (under !== h.wet) {
        h.wet = under;
        const sp = Math.abs(h.worldVel.y) + h.relVel.length() * 0.3;
        if (sp > 0.4 && Game.state === 'PLAYING') {
          AudioSys.wade(h.phys, clamp(sp / 3, 0.2, 1));
          Dust.emit(_gv.set(h.phys.x, this.level, h.phys.z), 5, 0.2, 0xd0e0e0, 0.9, 0.6, 0.6);
          Game.noise(h.phys, sp * 0.8, 'splash');
        }
      }
    }
    // under the surface: green-dark fog, muffled world, a drowning clock
    const under = Player.head.y < this.level - 0.02;
    if (under !== this.headUnder) {
      this.headUnder = under;
      const fog = Game.scene.fog;
      if (under && Game.state === 'PLAYING') { this.savedFogColor.copy(fog.color); this.savedFogDensity = fog.density; this.fogSaved = true; fog.color.setHex(0x0a2420); fog.density = 0.16; }
      else if (!under && this.fogSaved) { fog.color.copy(this.savedFogColor); fog.density = this.savedFogDensity; this.fogSaved = false; }
    }
    this.muffle = under ? 0.92 : 0;
    this.tint.visible = under; this.tint.material.opacity = under ? 0.35 : 0;
    if (under && Game.state === 'PLAYING' && !Player.god) {
      this.drownT += dt;
      if (Math.random() < dt * 3) Dust.emit(Player.head, 1, 0.1, 0xd8ffff, 0.8, 1.2, 0.1);   // your breath escaping
      if (this.drownT > U1.DROWN_TIME) { this.drownT = 0; Game.drown(); }
    } else this.drownT = Math.max(0, this.drownT - dt * 3);
  },
  restoreFog() { if (this.fogSaved) { Game.scene.fog.color.copy(this.savedFogColor); Game.scene.fog.density = this.savedFogDensity; this.fogSaved = false; this.headUnder = false; } },
};

/* =====================================================================
   8c. UPDATE 1 SYSTEMS — cords, lore notes, changing levels,
       the Heart, Time Trial ghosts, the hub, the cracking ground
   ===================================================================== */
const _hv = new THREE.Vector3(), _hw = new THREE.Vector3(), _hx = new THREE.Vector3(), _hy = new THREE.Vector3(), _hz = new THREE.Vector3();
const _hq = new THREE.Quaternion(), _hm = new THREE.Matrix4(), _hs = new THREE.Vector3();

// --------------------------------------------------------------- Cords (The Heart): grip and pull hard to snap them
class Cord {
  constructor(def, idx) {
    this.idx = idx;
    this.a = new THREE.Vector3().fromArray(def.a);           // wall end
    this.b = new THREE.Vector3().fromArray(def.b);           // heart end
    this.rest = new THREE.Vector3().fromArray(def.handle);   // the swollen knot you grab
    this.H = this.rest.clone();                              // knot as drawn (follows your pull)
    this.stage = def.stage || null; this.locked = !!def.locked; this.opens = def.opens || null;
    this.cut = false; this.cutT = 0; this.hand = null; this.grip = new THREE.Vector3(); this.pull = new THREE.Vector3();
    this.strain = 0; this.creakT = 0;
  }
  point(t, out) {   // quadratic through a (t=0), H (t=0.5), b (t=1)
    _hw.copy(this.H).multiplyScalar(2).addScaledVector(this.a, -0.5).addScaledVector(this.b, -0.5);
    const u = 1 - t;
    return out.copy(this.a).multiplyScalar(u * u).addScaledVector(_hw, 2 * u * t).addScaledVector(this.b, t * t);
  }
}
const Cords = {
  list: [], mesh: null, SEG: 18,
  setupLevel(data) {
    this.list.length = 0; this.mesh = null;
    const defs = data.cords || [];
    if (!defs.length) return;
    defs.forEach((d, i) => this.list.push(new Cord(d, i)));
    const geo = colorizeGeometry(new THREE.CylinderGeometry(1, 1, 1, 8, 1), 0xb05060, 0.1); geo.translate(0, -0.5, 0);
    this.mesh = new THREE.InstancedMesh(geo, getMaterial('flesh'), defs.length * this.SEG);
    this.mesh.frustumCulled = false; this.mesh.instanceMatrix.setUsage(THREE.DynamicDrawUsage);
    Level.root.add(this.mesh);
    this.render();
  },
  unlockStage(key) { for (const c of this.list) if (c.stage === key) c.locked = false; },
  remaining() { let n = 0; for (const c of this.list) if (!c.cut) n++; return n; },
  tryGrab(h) {
    const reach = Input.xr ? 0.3 : 0.7;
    for (const c of this.list) {
      if (c.cut || c.locked || c.hand || c.H.distanceTo(h.phys) > reach) continue;
      if (h.anchored) Player.release(h, false);
      c.hand = h; h.cord = c; c.grip.copy(h.phys); c.strain = 0;
      AudioSys.wetCreak(c.H, 0.5); Input.haptic(h.side, 0.5, 60);
      Game.toast(Input.xr ? 'PULL HARD' : 'HOLD THE MOUSE BUTTON TO PULL');
      return true;
    }
    return false;
  },
  letGo(c) { if (c.hand) { c.hand.cord = null; c.hand = null; } },
  update(dt) {
    if (!this.mesh) return;
    for (const c of this.list) {
      if (c.cut) { c.cutT += dt; continue; }
      if (!c.hand) { c.pull.multiplyScalar(Math.exp(-6 * dt)); c.H.copy(c.rest).add(c.pull); c.strain = Math.max(0, c.strain - dt); continue; }
      const h = c.hand;
      const desk = Input.desktopActive && !Input.xr;
      let stretch;
      if (desk) { stretch = U1.CORD_PULL_DIST + 0.1; _hv.set(0, 0, 0.45).applyQuaternion(Player.headWorldQuat); c.pull.lerp(_hv, 1 - Math.exp(-4 * dt)); }
      else { _hv.copy(h.tracked).sub(c.grip); stretch = _hv.length(); c.pull.copy(_hv).multiplyScalar(0.75); }
      c.H.copy(c.rest).add(c.pull);
      if (stretch > U1.CORD_MAX_STRETCH) { this.letGo(c); AudioSys.wetCreak(c.H, 0.4); Game.toast('YOUR GRIP SLIPS'); continue; }
      if (stretch > U1.CORD_PULL_DIST) {
        c.strain += dt;
        Input.haptic(h.side, 0.3 + c.strain * 0.5, 30);
        c.creakT -= dt;
        if (c.creakT <= 0) { c.creakT = 0.5; AudioSys.wetCreak(c.H, 0.4 + c.strain * 0.3); Dust.emit(c.H, 3, 0.2, 0x8a1020, -0.4, 1, 0.3); }
        if (c.strain >= U1.CORD_PULL_TIME * (desk ? 1.5 : 1)) this.snap(c);
      } else c.strain = Math.max(0, c.strain - dt * 0.5);
    }
    this.render();
  },
  snap(c) {
    this.letGo(c);
    c.cut = true; c.cutT = 0;
    AudioSys.snapCord(c.H);
    Input.hapticBoth(1, 350);
    Dust.emit(c.H, 40, 1.2, 0x7a0a18, 0.5, 2.5, 2);
    Subtitles.add('[a wet snap]', c.H);
    Game.onCordCut(c);
  },
  render() {
    let n = 0;
    const S = this.SEG;
    for (const c of this.list) {
      if (!c.cut) {
        for (let i = 0; i < S; i++) {
          c.point(i / S, _hx); c.point((i + 1) / S, _hy);
          const t = (i + 0.5) / S, r = Math.abs(t - 0.5) < 0.09 ? 0.22 : 0.13 + Math.sin(t * 40) * 0.01;   // the knot bulges
          n = this.seg(n, _hx, _hy, r);
        }
        continue;
      }
      // cut: the wall end dangles, the heart end whips back and is gone
      const sway = Math.sin(c.cutT * 2.2) * 0.4 * Math.exp(-c.cutT * 0.3);
      const L = c.a.distanceTo(c.rest);
      for (let i = 0; i < 6; i++) {
        _hx.copy(c.a).add(_hv.set(Math.sin(sway) * L * i / 6, -L * i / 6, 0));
        _hy.copy(c.a).add(_hv.set(Math.sin(sway) * L * (i + 1) / 6, -L * (i + 1) / 6, 0));
        n = this.seg(n, _hx, _hy, 0.13);
      }
      const k = Math.min(1, c.cutT / 1.2);
      if (k < 1) for (let i = 0; i < 6; i++) {
        _hx.lerpVectors(c.b, c.rest, (1 - k) * i / 6); _hy.lerpVectors(c.b, c.rest, (1 - k) * (i + 1) / 6);
        n = this.seg(n, _hx, _hy, 0.13 * (1 - k * 0.5));
      }
    }
    this.mesh.count = n;
    this.mesh.instanceMatrix.needsUpdate = true;
  },
  seg(idx, a, b, r) {
    _hv.copy(b).sub(a);
    const len = _hv.length();
    if (len < 1e-4) return idx;
    _hq.setFromUnitVectors(DOWN, _hv.multiplyScalar(1 / len));
    this.mesh.setMatrixAt(idx, _hm.compose(a, _hq, _hs.set(r, len + r * 0.6, r)));
    return idx + 1;
  },
};

// --------------------------------------------------------------- Lore notes: paper planes in a child's hand
const NOTE_TEXT = [
  'THE TALL MAN FIXED MY HORSE TOY. HE HAS TO BEND IN HALF TO FIT UNDER THE PLAYGROUND TREE. HE IS NICE.',
  'Mama says dont play here after the lamps go out. I asked who lights the lamps. She said HE does.',
  'THERE IS SINGING UNDER THE STREETS. THE TALL MAN PUTS HIS EAR ON THE GROUND AND LISTENS ALL NIGHT.',
  'He said the drains go down further than anybody dug. He said dont follow them. I followed them a little.',
  'We rang the bells so he would come and find us. It was a game. He always found us. He always laughed.',
  'He doesnt laugh now. His jaw hangs. Billy rang the bell and he came too fast.',
  'HE GOT TOO TALL FOR THE MILL DOOR SO HE CRAWLS NOW. HE SAID IT HURTS HIS BACK. SOMETHING MOVES ON HIS BACK.',
  'Papa says the ground is hungry and the tall man feeds it so it doesnt eat us. Papa says thats why he is so thin.',
  'Dont drop things in the well. Something drops them back up.',
  'I saw him climb down the well head first. He was crying I think. Do giants cry.',
  'THE HOUSES ARE EMPTY NOW. HE CARRIES US OUT ONE BY ONE. HE PUT ME ON THE LIGHTHOUSE STEPS AND WENT BACK.',
  'He went back for the last one. The last one was very small and had no legs. He made it from a toy.',
  'HE SLEEPS DOWN HERE ON OUR OLD BEDS AND CHAIRS. HE SLEEPS NEXT TO THE STONES THAT GLOW LIKE OUR LAMPS.',
  'The little white ones come out of his back when he is scared. They cant see. They listen. Be quiet be quiet be quiet.',
  'The water came up through the church floor. The tall man held up the bell tower with his hands for three days.',
  'He told me the bell is the only thing the heart is afraid of. Ring it and run up. Dont look at the water.',
  'There is a heart under the village. It has cords like roots. They go into him. He is not guarding us from it. He is holding it shut.',
  'If you cut the cords the heart lets go of him. He will be very tired. Tell him thank you. Tell him he can sleep.',
];
let NOTE_MAT = null;
class Note extends Interactable {
  constructor(def) {
    super();
    this.id = def.id;
    this.pos = new THREE.Vector3().fromArray(def.p);
    // settle onto whatever is underneath
    _hv.copy(this.pos); _hv.y += 0.4;
    if (World.raycast(_hv, DOWN, 3, null, _noteHit)) this.pos.y = _hv.y - _noteHit.t;
    this.group.position.copy(this.pos);
    this.group.rotation.y = (def.yaw !== undefined ? def.yaw : this.id * 47) * DEG;
    if (!NOTE_MAT) { NOTE_MAT = new THREE.MeshLambertMaterial({ map: getTexture('paper'), side: THREE.DoubleSide, emissive: 0x2a2620 }); NOTE_MAT.userData.shared = true; }
    // a folded paper plane: two wings and a keel
    const P = [0, 0.03, 0.13, -0.1, 0.035, -0.09, 0, 0.03, -0.09, 0, 0.03, 0.13, 0, 0.03, -0.09, 0.1, 0.035, -0.09,
      0, 0.03, 0.13, 0, 0.03, -0.09, 0, 0.005, -0.09];
    const UV = [0.5, 1, 0, 0, 0.5, 0, 0.5, 1, 0.5, 0, 1, 0, 0.5, 1, 0.5, 0, 0.3, 0];
    const geo = new THREE.BufferGeometry();
    geo.setAttribute('position', new THREE.Float32BufferAttribute(P, 3));
    geo.setAttribute('uv', new THREE.Float32BufferAttribute(UV, 2));
    geo.computeVertexNormals();
    this.plane = new THREE.Mesh(geo, NOTE_MAT);
    this.group.add(this.plane);
    this.t = Math.random() * 5; this.cool = 0;
  }
  update(dt) {
    this.t += dt; this.cool -= dt;
    this.plane.position.y = Math.sin(this.t * 1.5) * 0.01;
    this.plane.rotation.z = Math.sin(this.t * 1.1) * 0.06;
    if ((Game.state !== 'PLAYING' && Game.state !== 'MENU') || this.cool > 0) return;
    let hit = Player.head.distanceTo(this.pos) < (Input.xr ? 0.4 : 0.85);
    for (const h of Player.hands) if (h.phys.distanceTo(this.pos) < 0.2) hit = true;
    if (hit) { this.cool = 4; Notes.read(this.id); }
  }
}
const _noteHit = { t: 0, collider: null };
const Notes = {
  panel: null, showT: 0, at: new THREE.Vector3(),
  init(scene) {
    this.panel = new CanvasPanel(0.9, 0.66, 1024, 750, { renderOrder: 26 });
    this.panel.mesh.visible = false; scene.add(this.panel.mesh);
  },
  read(id) {
    const P = Game.progress;
    const first = !P.notes[id];
    P.notes[id] = true; Game.saveProgress();
    AudioSys.whoosh(Player.head, 0.15); AudioSys.chime(null, 0.2, 520);
    if (first) Game.toast(`NOTE FOUND  (${P.notes.filter(Boolean).length} / 18)`);
    Achievements.checkCollections();
    this.show(id, 0.75);
  },
  show(id, dist) {
    const text = NOTE_TEXT[id] || '';
    const rng = mulberry32(900 + id);
    const ink = ['#28305a', '#5a2420', '#2a4a2a', '#3a2a50'][id % 4];
    this.panel.draw((c, W, H) => {
      // crumpled lined paper
      c.fillStyle = '#e9e2cf'; c.fillRect(0, 0, W, H);
      c.strokeStyle = 'rgba(90,110,170,0.35)'; c.lineWidth = 2;
      for (let y = 90; y < H; y += 62) { c.beginPath(); c.moveTo(20, y); c.lineTo(W - 20, y); c.stroke(); }
      c.strokeStyle = 'rgba(180,60,60,0.35)'; c.beginPath(); c.moveTo(90, 0); c.lineTo(90, H); c.stroke();
      for (let i = 0; i < 6; i++) { c.strokeStyle = 'rgba(0,0,0,0.05)'; c.lineWidth = 3; c.beginPath(); c.moveTo(rng() * W, 0); c.lineTo(rng() * W, H); c.stroke(); }
      // big wobbly crayon letters
      c.fillStyle = ink; c.textBaseline = 'alphabetic';
      c.font = 'bold 50px "Comic Sans MS", "Chalkboard SE", "Marker Felt", "Segoe Print", cursive';
      const lines = wrapText(c, text, W - 170);
      let y = 80;
      for (const line of lines) {
        let x = 110;
        for (const word of line.split(' ')) {
          c.save(); c.translate(x, y + (rng() - 0.5) * 8); c.rotate((rng() - 0.5) * 0.08);
          c.fillText(word, 0, 0); c.restore();
          x += c.measureText(word + ' ').width + (rng() - 0.3) * 6;
        }
        y += 62;
      }
      // a little drawing in the corner: the tall man
      c.strokeStyle = ink; c.lineWidth = 4; c.beginPath();
      const bx = W - 120, by = H - 40;
      c.moveTo(bx - 25, by); c.lineTo(bx, by - 90); c.lineTo(bx + 25, by); c.moveTo(bx, by - 90); c.lineTo(bx, by - 170);
      c.moveTo(bx - 50, by - 100); c.lineTo(bx, by - 150); c.lineTo(bx + 50, by - 100);
      c.stroke(); c.beginPath(); c.arc(bx, by - 185, 15, 0, Math.PI * 2); c.stroke();
    });
    this.panel.mesh.visible = true;
    UI.placeInFront(this.panel.mesh, dist, -0.05);
    this.at.copy(Player.head);
    this.showT = 14;
  },
  hide() { this.panel.mesh.visible = false; this.showT = 0; },
  update(dt) {
    if (this.showT <= 0) return;
    this.showT -= dt;
    if (this.showT <= 0 || (Game.state === 'PLAYING' && Player.head.distanceTo(this.at) > 2.5)) this.hide();
  },
};

// --------------------------------------------------------------- Levels that change shape: rising paths and slammable platforms
class RevealGroup extends Interactable {
  constructor(key) {
    super();
    this.key = key; this.holder = new THREE.Group(); this.group.add(this.holder);
    this.holder.visible = false; this.revealed = false; this.done = false; this.t = 0;
  }
  reveal() {
    if (this.revealed) return;
    this.revealed = true; this.t = 0; this.holder.visible = true; this.holder.position.y = -5;
  }
  // a risen path can be torn down again later (the Heart crushes the way behind you)
  collapse() {
    if (!this.revealed || this.falling) return;
    this.falling = true; this.fallT = 0; this.vel = 0;
    for (const c of this.colliders) c.enabled = false;
    AudioSys.crash(Player.head, 0.6);
  }
  update(dt) {
    if (this.falling) {
      this.fallT += dt; this.vel += 9.8 * dt * 0.8;
      this.holder.position.y -= this.vel * dt;
      if (this.fallT > 3) this.holder.visible = false;
      return;
    }
    if (!this.revealed || this.done) return;
    this.t += dt;
    this.holder.position.y = -5 * (1 - smoothstep(0, 2.2, this.t));
    if (this.t >= 2.2) { this.done = true; for (const c of this.colliders) c.enabled = true; }
  }
}

// --------------------------------------------------------------- The Heart: a giant heartbeat that drives the light and the flesh
const Heart = {
  active: false, stopped: false, beatT: 0, beat: 0, fade: 1, light: null, mesh: null, center: new THREE.Vector3(),
  setupLevel(data) {
    FLESH_UNIFORMS.uPulse.value = 0;
    this.active = !!data.heart; this.stopped = false; this.fade = 1; this.beatT = 0; this.mesh = null; this.light = null;
    if (!this.active) return;
    const H = data.heart;
    this.center.fromArray(H.p);
    FLESH_UNIFORMS.uBreathCenter.value.copy(this.center);
    const r = H.r || 6, parts = [];
    for (const [x, y, z, s] of [[0, 0, 0, 1], [0.45, 0.35, 0.1, 0.7], [-0.4, 0.3, -0.15, 0.72], [0.1, -0.55, 0.15, 0.6], [-0.15, 0.75, 0.3, 0.45]]) {
      const g = colorizeGeometry(new THREE.SphereGeometry(r * s, 18, 14), 0xb04050, 0.15); g.translate(x * r, y * r, z * r); parts.push(g);
    }
    for (let i = 0; i < 6; i++) {   // arteries into the ceiling and floor
      const a = i / 6 * Math.PI * 2, up = i % 2 ? 1 : -1;
      const g = colorizeGeometry(new THREE.CylinderGeometry(r * 0.12, r * 0.2, r * 2.4, 8), 0x902838, 0.1);
      g.rotateZ(Math.cos(a) * 0.5); g.rotateX(Math.sin(a) * 0.5); g.translate(Math.cos(a) * r * 0.5, up * r * 1.3, Math.sin(a) * r * 0.5); parts.push(g);
    }
    const geo = mergeGeometries(parts); parts.forEach((g) => g.dispose());
    this.mesh = new THREE.Mesh(geo, getMaterial('flesh'));
    this.mesh.position.copy(this.center);
    Level.root.add(this.mesh);
    this.light = new THREE.PointLight(0xff2a1a, 0, 70, 1.1);
    this.light.position.copy(this.center); this.light.position.y += r + 1;
    Level.root.add(this.light);
  },
  stop() { this.stopped = true; },
  update(dt) {
    FLESH_UNIFORMS.uBreath.value += dt;
    if (!this.active) return;
    const period = 60 / U1.HEART_BPM;
    if (!this.stopped) {
      this.beatT += dt;
      if (this.beatT >= period) {
        this.beatT -= period;
        AudioSys.heartPulse(this.center, 1);
        Subtitles.add('[heartbeat]', this.center, 'heart');
        Input.hapticBoth(0.12, 60);
      }
    } else this.fade = Math.max(0, this.fade - dt * 0.25);
    const t = this.beatT;
    const env = Math.exp(-t * 6) + (t > 0.24 ? 0.7 * Math.exp(-(t - 0.24) * 6) : 0);   // lub-dub
    this.beat = this.stopped ? damp(this.beat, 0, 1.5, dt) : Math.min(1.2, env);
    FLESH_UNIFORMS.uPulse.value = this.beat * 0.35 * this.fade;
    this.light.intensity = (1.2 + this.beat * 5) * CONFIG.LIGHT_SCALE * (0.25 + 0.75 * this.fade);
    this.mesh.scale.setScalar(1 + this.beat * 0.05);
  },
};

// --------------------------------------------------------------- Time Trial ghost hands (recorded and replayed at 20 Hz)
const Ghost = {
  group: null, parts: [], crown: null, rec: null, recN: 0, recT: 0, play: null, playN: 0, origin: new THREE.Vector3(), on: false,
  init(scene) {
    const mat = new THREE.MeshBasicMaterial({ color: 0x9ad8ff, transparent: true, opacity: 0.3, depthWrite: false, blending: THREE.AdditiveBlending, fog: false });
    mat.userData.shared = true;
    this.group = new THREE.Group(); this.group.visible = false; scene.add(this.group);
    for (let s = 0; s < 2; s++) {
      const hand = buildHandModel(s, { fingers: [], thumb: null });
      hand.traverse((o) => { if (o.isMesh) { o.material.dispose(); o.material = mat; } });
      this.group.add(hand); this.parts.push(hand);
    }
    const head = new THREE.Mesh(new THREE.SphereGeometry(0.12, 12, 8), mat); this.group.add(head); this.parts.push(head);
    this.crown = makeCrown(PropMat.basic(0xffd060, 'crownGhost'));
    this.group.add(this.crown);
  },
  key(i) { return 'hollowmaw_ghost_' + i; },
  start() {
    this.on = Game.mode === 'timetrial';
    this.group.visible = false;
    if (!this.on) { this.rec = null; this.play = null; return; }
    this.origin.fromArray(Level.data.spawn.p);
    if (!this.rec) this.rec = new Int16Array(U1.GHOST_HZ * U1.GHOST_MAX_SECONDS * 9);
    this.recN = 0; this.recT = 0;
    this.play = null; this.playN = 0;
    try {
      const s = localStorage.getItem(this.key(Game.levelIndex));
      if (s) { this.play = this.decode(s); this.playN = Math.floor(this.play.length / 9); }
    } catch (e) { this.play = null; }
    this.crown.visible = !!Game.progress.cosmetics.crown;
  },
  sample(p, i) {
    const o = this.origin, R = this.rec;
    R[i] = clamp(Math.round((p.x - o.x) * 100), -32767, 32767);
    R[i + 1] = clamp(Math.round((p.y - o.y) * 100), -32767, 32767);
    R[i + 2] = clamp(Math.round((p.z - o.z) * 100), -32767, 32767);
  },
  read(f, k, out) {
    const P = this.play, i = f * 9 + k * 3, o = this.origin;
    return out.set(P[i] / 100 + o.x, P[i + 1] / 100 + o.y, P[i + 2] / 100 + o.z);
  },
  update(dt) {
    if (!this.on || Game.state !== 'PLAYING') { this.group.visible = false; return; }
    // record
    const step = 1 / U1.GHOST_HZ;
    this.recT += dt;
    while (this.recT >= step && (this.recN + 1) * 9 <= this.rec.length) {
      this.recT -= step;
      const i = this.recN * 9;
      this.sample(Player.head, i); this.sample(Player.hands[0].phys, i + 3); this.sample(Player.hands[1].phys, i + 6);
      this.recN++;
    }
    // replay the best run
    if (!this.play || this.playN < 2) { this.group.visible = false; return; }
    const f = Game.stats.time * U1.GHOST_HZ;
    const i0 = Math.min(this.playN - 1, Math.floor(f)), i1 = Math.min(this.playN - 1, i0 + 1), a = clamp(f - i0, 0, 1);
    this.group.visible = true;
    for (let k = 0; k < 3; k++) {
      this.read(i0, k, _hv); this.read(i1, k, _hw);
      this.parts[k === 0 ? 2 : k - 1].position.lerpVectors(_hv, _hw, a);
    }
    this.parts[0].quaternion.copy(Player.hands[0].worldQuat); this.parts[1].quaternion.copy(Player.hands[1].worldQuat);
    this.crown.position.copy(this.parts[2].position); this.crown.position.y += 0.1;
  },
  save() {
    if (!this.rec || this.recN < 2) return;
    try { localStorage.setItem(this.key(Game.levelIndex), this.encode(this.rec.subarray(0, this.recN * 9))); } catch (e) { /* storage full or unavailable */ }
  },
  encode(arr) {
    const u8 = new Uint8Array(arr.buffer, arr.byteOffset, arr.byteLength);
    let s = '';
    for (let i = 0; i < u8.length; i += 0x8000) s += String.fromCharCode.apply(null, u8.subarray(i, i + 0x8000));
    return btoa(s);
  },
  decode(b64) {
    const s = atob(b64), u8 = new Uint8Array(s.length - (s.length % 2));
    for (let i = 0; i < u8.length; i++) u8[i] = s.charCodeAt(i);
    return new Int16Array(u8.buffer);
  },
};
function makeCrown(mat) {
  const parts = [[new THREE.CylinderGeometry(0.085, 0.08, 0.05, 12, 1, true)]];
  for (let i = 0; i < 5; i++) { const a = i / 5 * Math.PI * 2; parts.push([new THREE.ConeGeometry(0.018, 0.06, 4), Math.cos(a) * 0.08, 0.05, Math.sin(a) * 0.08]); }
  const m = mergeInto(new THREE.Group(), mat, parts);
  m.removeFromParent();
  return m;
}

// --------------------------------------------------------------- The hub (Playground): the Shelf, a mirror, the achievements board
const Hub = {
  active: false, board: null, boardCtx: null, boardTex: null, shelf: null, items: [], labelCtx: null, labelTex: null,
  mirror: null, puppet: null, mirrorN: new THREE.Vector3(), mirrorP: new THREE.Vector3(),
  build(data) {
    this.active = !!data.hub;
    this.items.length = 0; this.board = null; this.puppet = null;
    if (!this.active) return;
    const H = data.hub;
    // achievements board
    const bc = makeCanvas(1024, 760);
    this.boardCtx = bc.getContext('2d');
    this.boardTex = new THREE.CanvasTexture(bc); this.boardTex.colorSpace = THREE.SRGBColorSpace;
    const bg = new THREE.Group(); bg.position.fromArray(H.board.p); bg.rotation.y = H.board.yaw * DEG; Level.root.add(bg);
    bg.add(new THREE.Mesh(colorizeGeometry(new THREE.BoxGeometry(1.6, 1.2, 0.05), 0x4a3424), getMaterial('wood')));
    const face = new THREE.Mesh(new THREE.PlaneGeometry(1.5, 1.1), new THREE.MeshBasicMaterial({ map: this.boardTex }));
    face.position.z = 0.03; bg.add(face);
    for (const x of [-0.7, 0.7]) { const post = new THREE.Mesh(colorizeGeometry(new THREE.CylinderGeometry(0.04, 0.04, 2.4, 6), 0x3a2a1c), getMaterial('wood')); post.position.set(x, -0.6, -0.04); bg.add(post); }
    this.board = bg;
    // the Shelf: one display per cosmetic, locked ones dark
    const sg = new THREE.Group(); sg.position.fromArray(H.shelf.p); sg.rotation.y = H.shelf.yaw * DEG; Level.root.add(sg);
    const wood = [];
    for (const y of [0.05, 0.6, 1.15, 1.7]) wood.push([colorizeGeometry(new THREE.BoxGeometry(1.5, 0.05, 0.4), 0x5a3e28), 0, y, 0]);
    for (const x of [-0.75, 0.75]) wood.push([colorizeGeometry(new THREE.BoxGeometry(0.05, 1.7, 0.4), 0x4a3220), x, 0.875, 0]);
    wood.push([colorizeGeometry(new THREE.BoxGeometry(1.5, 1.7, 0.03), 0x3a2618), 0, 0.875, -0.2]);
    mergeInto(sg, getMaterial('wood'), wood);
    addShelfCollider(sg);
    COSMETICS.forEach((c, i) => {
      const x = -0.5 + (i % 3) * 0.5, y = 0.08 + Math.floor(i / 3) * 0.55;
      let mesh;
      if (c.kind === 'fur') mesh = new THREE.Mesh(new THREE.SphereGeometry(0.09, 14, 10), new THREE.MeshLambertMaterial({ map: getTexture(c.tex) }));
      else if (c.kind === 'bracelet') { mesh = new THREE.Mesh(new THREE.TorusGeometry(0.07, 0.014, 6, 18), new THREE.MeshLambertMaterial({ color: 0xc8a040 })); mesh.rotation.x = 0.4; }
      else if (c.kind === 'lantern') mesh = new THREE.Mesh(new THREE.BoxGeometry(0.1, 0.14, 0.1), new THREE.MeshLambertMaterial({ color: 0x3a3028, emissive: 0x000000 }));
      else mesh = makeCrown(new THREE.MeshLambertMaterial({ color: 0xd8b040 }));
      mesh.position.set(x, y + 0.12, 0.02);
      sg.add(mesh);
      this.items.push({ c, mesh });
    });
    const lc = makeCanvas(1024, 1024);
    this.labelCtx = lc.getContext('2d');
    this.labelTex = new THREE.CanvasTexture(lc); this.labelTex.colorSpace = THREE.SRGBColorSpace;
    const label = new THREE.Mesh(new THREE.PlaneGeometry(1.5, 1.5), new THREE.MeshBasicMaterial({ map: this.labelTex, transparent: true }));
    label.position.set(0, 0.95, 0.205); sg.add(label);
    this.shelf = sg;
    // the mirror: a dark glass that shows a little puppet of you
    const mg = new THREE.Group(); mg.position.fromArray(H.mirror.p); mg.rotation.y = H.mirror.yaw * DEG; Level.root.add(mg);
    mergeInto(mg, getMaterial('wood'), [[colorizeGeometry(new THREE.BoxGeometry(1.5, 0.08, 0.08), 0x6a4a2a), 0, 1.84, 0], [colorizeGeometry(new THREE.BoxGeometry(1.5, 0.08, 0.08), 0x6a4a2a), 0, 0.04, 0],
      [colorizeGeometry(new THREE.BoxGeometry(0.08, 1.88, 0.08), 0x6a4a2a), -0.75, 0.94, 0], [colorizeGeometry(new THREE.BoxGeometry(0.08, 1.88, 0.08), 0x6a4a2a), 0.75, 0.94, 0]]);
    const glass = new THREE.Mesh(new THREE.PlaneGeometry(1.42, 1.76), new THREE.MeshBasicMaterial({ color: 0x0e161c }));
    glass.position.set(0, 0.94, -0.01); mg.add(glass);
    this.mirrorP.fromArray(H.mirror.p); this.mirrorN.set(Math.sin(H.mirror.yaw * DEG), 0, Math.cos(H.mirror.yaw * DEG));
    this.mirrorP.addScaledVector(this.mirrorN, -0.01);
    const pg = new THREE.Group(); pg.visible = false; Level.root.add(pg);
    const pz = [];
    for (let s = 0; s < 2; s++) {   // the puppet's left hand is a mirrored right hand
      const hand = buildHandModel(1 - s, { fingers: [], thumb: null });
      const pmat = Player.hands[1 - s].visual.children[0].material;
      hand.traverse((o) => { if (o.isMesh) { o.material.dispose(); o.material = pmat; } });
      pg.add(hand); pz.push(hand);
    }
    const body = new THREE.Mesh(new THREE.SphereGeometry(0.3, 16, 12), Player.hands[0].visual.children[0].material);
    pg.add(body); pz.push(body);
    const crown = makeCrown(PropMat.lambert(0xd8b040, 'crownGold')); pg.add(crown); pz.push(crown);
    this.puppet = { group: pg, parts: pz };
    this.refreshBoard(); this.refreshShelf();
  },
  reflect(p, out) { const d = _hv.copy(p).sub(this.mirrorP).dot(this.mirrorN); return out.copy(p).addScaledVector(this.mirrorN, -2 * d); },
  reflectDir(v, out) { return out.copy(v).addScaledVector(this.mirrorN, -2 * v.dot(this.mirrorN)); },
  update() {
    if (!this.active || !this.puppet) return;
    const d = _hv.copy(Player.head).sub(this.mirrorP).dot(this.mirrorN);
    const near = d > 0.1 && d < 4 && Player.head.distanceTo(this.mirrorP) < 5;
    const P = this.puppet;
    P.group.visible = near;
    if (!near) return;
    for (let s = 0; s < 2; s++) {
      const v = Player.hands[s].visual, ph = P.parts[s];
      ph.visible = v.visible;
      this.reflect(v.position, ph.position);
      _hm.makeRotationFromQuaternion(v.quaternion).extractBasis(_hx, _hy, _hz);
      this.reflectDir(_hx, _hx).negate(); this.reflectDir(_hy, _hy); this.reflectDir(_hz, _hz);
      _hm.makeBasis(_hx, _hy, _hz); ph.quaternion.setFromRotationMatrix(_hm);
    }
    this.reflect(_hw.copy(Player.head).setY(Player.head.y + CONFIG.BODY_OFFSET_Y), P.parts[2].position);
    this.reflect(_hw.copy(Player.head).setY(Player.head.y + 0.02), P.parts[3].position);
    P.parts[3].visible = !!Game.progress.cosmetics.crown;
  },
  refreshBoard() {
    if (!this.active || !this.boardCtx) return;
    const c = this.boardCtx, W = 1024, H = 760;
    c.fillStyle = '#16100c'; c.fillRect(0, 0, W, H);
    c.fillStyle = '#f0c890'; c.font = 'bold 54px Georgia'; c.textAlign = 'center'; c.fillText('ACHIEVEMENTS', W / 2, 64);
    c.font = '24px Georgia'; c.fillStyle = '#a08870'; c.fillText(`${Achievements.count()} / ${ACHIEVEMENTS.length}`, W / 2, 98);
    ACHIEVEMENTS.forEach((a, i) => {
      const col = i % 2, row = Math.floor(i / 2), x = 40 + col * 495, y = 150 + row * 86;
      const got = Achievements.has(a.id);
      c.textAlign = 'left';
      c.fillStyle = got ? '#ffd27a' : '#5a4a3c'; c.font = 'bold 30px Georgia'; c.fillText((got ? '★ ' : '☆ ') + a.name, x, y);
      c.fillStyle = got ? '#c8b498' : '#6a5a4a'; c.font = 'italic 20px Georgia';
      drawTextBlock(c, a.hint, x + 34, y + 28, 440, 22, 'left');
    });
    this.boardTex.needsUpdate = true;
  },
  refreshShelf() {
    if (!this.active || !this.labelCtx) return;
    const toys = Cosmetics.toys();
    for (const it of this.items) {
      const ok = Cosmetics.unlocked(it.c), on = Cosmetics.equipped(it.c);
      it.mesh.traverse((o) => { if (o.isMesh) { o.material.color.setScalar(ok ? 1 : 0.08); if (o.material.emissive) o.material.emissive.setHex(on ? 0x3a2a10 : 0x000000); } });
      it.mesh.scale.setScalar(on ? 1.25 : 1);
    }
    const c = this.labelCtx, S = 1024;
    c.clearRect(0, 0, S, S);
    c.textAlign = 'center';
    c.fillStyle = 'rgba(14,10,8,0.85)'; c.fillRect(150, 8, 724, 64);
    c.fillStyle = '#f0c890'; c.font = 'bold 40px Georgia'; c.fillText(`THE SHELF   ·   TOYS ${toys} / 9`, S / 2, 54);
    this.items.forEach((it, i) => {
      const x = S / 2 + (-0.5 + (i % 3) * 0.5) / 1.5 * S, y = S - (0.08 + Math.floor(i / 3) * 0.55) / 1.5 * S - 4;
      const ok = Cosmetics.unlocked(it.c);
      c.fillStyle = 'rgba(14,10,8,0.8)'; c.fillRect(x - 150, y - 34, 300, 40);
      c.fillStyle = ok ? (Cosmetics.equipped(it.c) ? '#ffd27a' : '#e8dcc8') : '#7a6a5a';
      c.font = 'bold 26px Georgia';
      c.fillText(ok ? it.c.name : `${it.c.toys} TOYS TO UNLOCK`, x, y - 6);
    });
    this.labelTex.needsUpdate = true;
  },
};
function addShelfCollider(g) {
  g.updateMatrixWorld(true);
  const q = g.getWorldQuaternion(_hq), p = g.getWorldPosition(_hv);
  const c = World.makeBox(_hw.set(0, 0.875, -0.05).applyQuaternion(q).add(p), q, _hx.set(0.78, 0.875, 0.2));
  World.add(c);
}

// --------------------------------------------------------------- The first ending: the ground behind the gate cracks open
const Crack = {
  mesh: null, t: -1, center: new THREE.Vector3(), rumbleT: 0,
  start(p) {
    const S = 512, c = makeCanvas(S, S), ctx = c.getContext('2d'), r = mulberry32(77);
    ctx.lineCap = 'round';
    const branch = (x, y, a, len, w, depth) => {
      for (let i = 0; i < len; i++) {
        const nx = x + Math.cos(a) * 9, ny = y + Math.sin(a) * 9;
        ctx.strokeStyle = 'rgba(120,20,10,0.5)'; ctx.lineWidth = w + 6; ctx.beginPath(); ctx.moveTo(x, y); ctx.lineTo(nx, ny); ctx.stroke();
        ctx.strokeStyle = '#000'; ctx.lineWidth = w; ctx.beginPath(); ctx.moveTo(x, y); ctx.lineTo(nx, ny); ctx.stroke();
        x = nx; y = ny; a += (r() - 0.5) * 0.6; w = Math.max(1, w * 0.97);
        if (depth < 3 && r() < 0.08) branch(x, y, a + (r() - 0.5) * 1.6, len - i, w * 0.6, depth + 1);
      }
    };
    for (let k = 0; k < 7; k++) branch(S / 2, S / 2, k / 7 * Math.PI * 2 + r(), 26, 14, 0);
    const tex = new THREE.CanvasTexture(c); tex.colorSpace = THREE.SRGBColorSpace;
    this.mesh = new THREE.Mesh(new THREE.PlaneGeometry(1, 1), new THREE.MeshBasicMaterial({ map: tex, transparent: true, depthWrite: false, polygonOffset: true, polygonOffsetFactor: -2, fog: false }));
    this.mesh.rotation.x = -Math.PI / 2; this.mesh.position.copy(p); this.mesh.scale.setScalar(0.1);
    Level.root.add(this.mesh);
    this.center.copy(p); this.t = 0; this.rumbleT = 0;
    AudioSys.crash(p, 0.8); AudioSys.thud(p, 1.5);
    Subtitles.add('[the ground splits open]', p);
  },
  update(dt) {
    if (this.t < 0 || !this.mesh || !this.mesh.parent) { this.t = -1; return; }
    this.t += dt;
    this.mesh.scale.setScalar(0.1 + 16 * smoothstep(0, 4.5, this.t));
    this.rumbleT -= dt;
    if (this.rumbleT <= 0 && this.t < 6) {
      this.rumbleT = 0.5 + Math.random() * 0.6;
      _hv.copy(this.center).add(_hw.set((Math.random() - 0.5) * 12, 0.2, (Math.random() - 0.5) * 12));
      AudioSys.thud(_hv, 0.6); Dust.emit(_hv, 14, 2, 0x5a4a3a, 0.6, 2, 0.6);
      Input.hapticBoth(0.4, 160);
    }
  },
};
```

## PATCH #75 — 9. LEVEL DATA: stage:'key' + reveal:true (rises in later) or collapse (falls away),

FIND:
```js
/* =====================================================================
   9. LEVEL DATA — levels 0–5 as primitive definitions
   Prim: { t:'box'|'cyl'|'plane', p:[x,y,z], s:[w,h,d] | [r,h] | [w,d],
           r:[deg x,y,z] or q:[x,y,z,w], c:color, m:material, surf, col:false,
           inst:'key' (instanced), roof:id (collapsible), pass/block (Warden) }
   ===================================================================== */
```
REPLACE WITH:
```js
/* =====================================================================
   9. LEVEL DATA — levels 0–5 as primitive definitions
   Prim: { t:'box'|'cyl'|'plane'|'cone', p:[x,y,z], s:[w,h,d] | [r,h] | [w,d] | [rTop,rBottom,h],
           r:[deg x,y,z] or q:[x,y,z,w], c:color, m:material, surf, col:false,
           inst:'key' (instanced), roof:id (collapsible), pass/block (Warden),
           UPDATE 1: stage:'key' + reveal:true (rises in later) or collapse (falls away),
           slam:'id' (a platform the Warden can smash) }
   UPDATE 1 level fields: props, hides, notes, crawlers, peeks, water, cords, heart, pits, hub
   ===================================================================== */
```

## PATCH #76 — 9. LEVEL DATA: the hub — notes, throwing and hiding practice, the Shelf, a mirror, the achievements board

FIND:
```js
      { p: [0, 1.6, -16.4], yaw: 0, w: 1.8, h: 1.1, text: 'LANTERNS SAVE YOUR PROGRESS\nClimb the treehouse - the rope and bark are easy to grip - and touch its lantern.' },
      { p: [8, 1.1, 6.3], yaw: 180, w: 1.5, h: 0.9, text: 'THE DRAIN\nIt opens when the treehouse lantern burns. Go down into the dark.' },
    ],
    menu: { p: [0, 1.2, 4.6], yaw: 0 },
    warden: { mode: 'silhouette', ground: 0, walkSpeed: 2.6, canSee: false, canCatch: false, hearing: 0, path: [[-140, 0, -66], [-40, 0, -62], [40, 0, -62], [140, 0, -66]], breath: 0 },
```
REPLACE WITH:
```js
      { p: [0, 1.6, -16.4], yaw: 0, w: 1.8, h: 1.1, text: 'LANTERNS SAVE YOUR PROGRESS\nClimb the treehouse - the rope and bark are easy to grip - and touch its lantern.' },
      { p: [8, 1.1, 6.3], yaw: 180, w: 1.5, h: 0.9, text: 'THE DRAIN\nIt opens when the treehouse lantern burns. Go down into the dark.' },
      { p: [2.9, 1.15, 7.6], yaw: -90, w: 1.5, h: 0.9, text: 'THROWING\nGrip a bottle, can or stone to pick it up. Let go mid-swing to throw it. Things go to listen where it lands.' },
      { p: [-3.4, 1.15, 8.6], yaw: 90, w: 1.5, h: 0.9, text: 'HIDING\nTouch the door, climb in, and it pulls shut. Hold still in there. It may come and open it.' },
      { p: [-11.3, 2.1, 1.8], yaw: 90, w: 1.4, h: 0.8, text: 'THE SHELF\nEvery carved toy you find unlocks something to wear. Choose on the menu board.' },
      ...(Game.progress.endings.first ? [{ p: [9.4, 1.0, -6], yaw: -90, w: 1.4, h: 0.8, text: 'THE HOLE\nThe ground opened when you escaped. It goes down. Further than anyone dug.' }] : []),
    ],
    menu: { p: [0, 1.2, 4.6], yaw: 0 },
    // UPDATE 1: the hub — notes, throwing and hiding practice, the Shelf, a mirror, the achievements board,
    // and (after the first ending) a hole that leads down into The Deeper Dark
    notes: [{ id: 0, p: [-7.5, 0.3, 1.4] }, { id: 1, p: [-1.2, 4.9, tz + 1.3] }],
    props: [{ type: 'stone', p: [2.2, 0.3, 6.6] }, { type: 'stone', p: [2.6, 0.3, 6.2] }, { type: 'bottle', p: [3.0, 0.3, 6.8] }, { type: 'can', p: [3.4, 0.3, 6.3] }],
    hides: [{ type: 'locker', p: [-4.6, 0, 8.7], yaw: 180 }],
    hub: { board: { p: [2.45, 1.25, 4.8], yaw: -12 }, shelf: { p: [-11.6, 0, 3.5], yaw: 90 }, mirror: { p: [-11.6, 0, -6.5], yaw: 90 } },
    pits: Game.progress.endings.first ? [{ type: 'pit', p: [11, 0, -6], r: 1.4, trigger: { p: [11, 0.2, -6], h: [1.1, 0.8, 1.1] } }] : [],
    warden: { mode: 'silhouette', ground: 0, walkSpeed: 2.6, canSee: false, canCatch: false, hearing: 0, path: [[-140, 0, -66], [-40, 0, -62], [40, 0, -62], [140, 0, -66]], breath: 0 },
```

## PATCH #77 — 9. LEVEL DATA: notes and things to throw

FIND:
```js
  const wp = [];
  for (let x = -18; x <= 18; x += 12) for (let z = -30; z <= 30; z += 12) wp.push([x, 0, z]);
  return {
    name: 'THE DRAINS', subtitle: 'it walks above you', index: 1,
```
REPLACE WITH:
```js
  const wp = [];
  for (let x = -18; x <= 18; x += 12) for (let z = -30; z <= 30; z += 12) wp.push([x, 0, z]);
  // UPDATE 1: notes and things to throw
  const notes = [{ id: 2, p: [cx(12), 0.3, cz(16)] }, { id: 3, p: [cx(2), 0.3, cz(11)] }];
  const props = [{ type: 'can', p: [0.6, 0.3, cz(18)] }, { type: 'bottle', p: [-0.8, 0.3, cz(15)] }, { type: 'stone', p: [0.5, 0.3, cz(13)] }, { type: 'can', p: [cx(12), 0.3, cz(4)] }];
  return {
    notes, props,
    name: 'THE DRAINS', subtitle: 'it walks above you', index: 1,
```

## PATCH #78 — 9. LEVEL DATA: const notes = [{ id: 4, p: [plats.A[0] - 1.1, plats.A[1] + 0.3, plats.A[2] - 0.6] }, { id:

FIND:
```js
  pickups.push({ type: 'battery', p: [plats.S[0] - 1, plats.S[1] + 0.13, plats.S[2] + 1] }, { type: 'battery', p: [plats.C[0] - 1, plats.C[1] + 0.13, plats.C[2] + 1] }, { type: 'battery', p: [plats.G[0] - 1, plats.G[1] + 0.13, plats.G[2] + 1] });
  pickups.push({ type: 'toy', p: [plats.T[0] + 1, plats.T[1] + 0.13, plats.T[2] + 1] });
  return {
    name: 'THE CANOPY', subtitle: 'it looks up', index: 2,
```
REPLACE WITH:
```js
  pickups.push({ type: 'battery', p: [plats.S[0] - 1, plats.S[1] + 0.13, plats.S[2] + 1] }, { type: 'battery', p: [plats.C[0] - 1, plats.C[1] + 0.13, plats.C[2] + 1] }, { type: 'battery', p: [plats.G[0] - 1, plats.G[1] + 0.13, plats.G[2] + 1] });
  pickups.push({ type: 'toy', p: [plats.T[0] + 1, plats.T[1] + 0.13, plats.T[2] + 1] });
  // UPDATE 1
  const notes = [{ id: 4, p: [plats.A[0] - 1.1, plats.A[1] + 0.3, plats.A[2] - 0.6] }, { id: 5, p: [plats.G[0] + 0.8, plats.G[1] + 0.3, plats.G[2] + 0.9] }];
  const props = [{ type: 'bottle', p: [plats.S[0] + 1, plats.S[1] + 0.3, plats.S[2] + 1] }, { type: 'bottle', p: [plats.C[0] + 1, plats.C[1] + 0.3, plats.C[2] - 1] },
    { type: 'stone', p: [plats.D[0] - 1, plats.D[1] + 0.3, plats.D[2] + 1] }, { type: 'stone', p: [plats.E[0] - 1, plats.E[1] + 0.3, plats.E[2] - 1] }, { type: 'can', p: [plats.B[0] + 1, plats.B[1] + 0.3, plats.B[2] + 1] }];
  return {
    notes, props,
    name: 'THE CANOPY', subtitle: 'it looks up', index: 2,
```

## PATCH #79 — 9. LEVEL DATA: the east wall has two windows the Warden can put its eye to

FIND:
```js
  P.push(box([0, 7, -18.5], [52, 14, 1], 'wood', WALL));
  P.push(box([-25.5, 7, 0], [1, 14, 38], 'wood', WALL));
  P.push(box([25.5, 7, 0], [1, 14, 38], 'wood', WALL));
  P.push(box([-14.75, 7, 18.5], [21.5, 14, 1], 'wood', WALL));
```
REPLACE WITH:
```js
  P.push(box([0, 7, -18.5], [52, 14, 1], 'wood', WALL));
  P.push(box([-25.5, 7, 0], [1, 14, 38], 'wood', WALL));
  // UPDATE 1: the east wall has two windows the Warden can put its eye to
  P.push(box([25.5, 4.3, 0], [1, 8.6, 38], 'wood', WALL));
  P.push(box([25.5, 12.2, 0], [1, 3.6, 38], 'wood', WALL));
  for (const [z0, z1] of [[-19, -9], [-7, 7], [9, 19]]) P.push(box([25.5, 9.5, (z0 + z1) / 2], [1, 1.8, z1 - z0], 'wood', WALL));
  P.push(box([-14.75, 7, 18.5], [21.5, 14, 1], 'wood', WALL));
```

## PATCH #80 — 9. LEVEL DATA: const notes = [{ id: 6, p: [-23.7, 4.3, 2.5] }, { id: 7, p: [18, 0.3, -14] }];

FIND:
```js
  pickups.push({ type: 'battery', p: [-23.5, 4.0, 6] }, { type: 'battery', p: [8, 0.05, 14] });
  pickups.push({ type: 'toy', p: [20, 3.66, -13] });
  const wp = [[0, 0, 34], [30, 0, 32], [36, 0, 0], [30, 0, -32], [0, 0, -34], [-34, 0, -30], [-36, 0, 0], [-30, 0, 32], [0, 0, 24], [0, 0, 11], [-10, 0, 5], [10, 0, 5], [-11, 0, -7], [9, 0, -7], [0, 0, -12]];
  return {
    name: 'THE MILL', subtitle: 'it crawls inside', index: 3,
```
REPLACE WITH:
```js
  pickups.push({ type: 'battery', p: [-23.5, 4.0, 6] }, { type: 'battery', p: [8, 0.05, 14] });
  pickups.push({ type: 'toy', p: [20, 3.66, -13] });
  // UPDATE 1
  const notes = [{ id: 6, p: [-23.7, 4.3, 2.5] }, { id: 7, p: [18, 0.3, -14] }];
  const props = [{ type: 'bottle', p: [5, 0.3, 4] }, { type: 'bottle', p: [-10, 0.3, 8] }, { type: 'can', p: [12, 0.3, -2] }, { type: 'can', p: [-3, 8.3, 0] },
    { type: 'stone', p: [-16, 0.3, 4] }, { type: 'flare', p: [6.5, 0.3, 14.5] }];
  const hides = [{ type: 'locker', p: [-8, 0, 17.45], yaw: 180 }, { type: 'locker', p: [-9.2, 0, 17.45], yaw: 180 }, { type: 'barrel', p: [9, 0, -16.4] }];
  const peeks = [{ eye: [26.7, 9.5, -8], look: [22, 8.6, -8] }, { eye: [26.7, 9.5, 8], look: [22, 8.6, 8] }];
  const wp = [[0, 0, 34], [30, 0, 32], [36, 0, 0], [30, 0, -32], [0, 0, -34], [-34, 0, -30], [-36, 0, 0], [-30, 0, 32], [0, 0, 24], [0, 0, 11], [-10, 0, 5], [10, 0, 5], [-11, 0, -7], [9, 0, -7], [0, 0, -12]];
  return {
    notes, props, hides, peeks,
    name: 'THE MILL', subtitle: 'it crawls inside', index: 3,
```

## PATCH #81 — 9. LEVEL DATA: edit: const wellNotes = [];

INSERT AFTER:
```js
  // spiral of ledges
  let rest = [];
  for (let k = 0; k < 32; k++) {
```
NEW CODE:
```js
  const wellNotes = [];
```

## PATCH #82 — 9. LEVEL DATA: UPDATE 1

INSERT AFTER:
```js
    if (k === 4 || k === 14) pickups.push({ type: 'battery', p: wallPos(th + 0.05, y + 0.16, R - 0.7) });
    if (k === 13) pickups.push({ type: 'toy', p: wallPos(th - 0.06, y + 0.16, R - 0.5) });
  }
```
NEW CODE:
```js
    if (k === 7 || k === 22) wellNotes.push({ id: k === 7 ? 8 : 9, p: wallPos(th + 0.08, y + 0.4, R - 0.75) });   // UPDATE 1
```

## PATCH #83 — 9. LEVEL DATA: edit: notes: wellNotes,

INSERT AFTER:
```js
  }
  return {
    name: 'THE WELL', subtitle: 'it comes down', index: 4,
```
NEW CODE:
```js
    notes: wellNotes,
```

## PATCH #84 — 9. LEVEL DATA: const notes = [{ id: 10, p: onRoof(house(6, 1), -1, 0, 0.3) }, { id: 11, p: onRoof(house(1

FIND:
```js
  pickups.push({ type: 'toy', p: onRoof(house(6, -1), 1.5, 3.2, 0.02) });
  const spawnP = onRoof(house(0, 1), 0, 1.5, 0.7);
  return {
    name: 'THE ESCAPE', subtitle: 'run', index: 5,
```
REPLACE WITH:
```js
  pickups.push({ type: 'toy', p: onRoof(house(6, -1), 1.5, 3.2, 0.02) });
  const spawnP = onRoof(house(0, 1), 0, 1.5, 0.7);
  // UPDATE 1
  const notes = [{ id: 10, p: onRoof(house(6, 1), -1, 0, 0.3) }, { id: 11, p: onRoof(house(12, -1), 0, 2, 0.3) }];
  const props = [{ type: 'bottle', p: onRoof(house(3, 1), -1.5, -2, 0.3) }, { type: 'bottle', p: onRoof(house(9, -1), 1, 1, 0.3) }];
  return {
    notes, props,
    name: 'THE ESCAPE', subtitle: 'run', index: 5,
```

## PATCH #85 — 9. LEVEL DATA: whole section: 9b. LEVEL DATA (UPDATE 1) — THE DEEPER DARK: levels 6–8 and the

FIND:
```js
}

const LEVELS = [levelPlayground, levelDrains, levelCanopy, levelMill, levelWell, levelEscape];
const LEVEL_NAMES = ['THE PLAYGROUND', 'THE DRAINS', 'THE CANOPY', 'THE MILL', 'THE WELL', 'THE ESCAPE'];

```
REPLACE WITH:
```js
}


/* =====================================================================
   9b. LEVEL DATA (UPDATE 1) — THE DEEPER DARK: levels 6–8 and the
       Endless Descent generator. Same primitive format as levels 0–5.
   ===================================================================== */
const cone = (p, rTop, rBottom, h, m, c, o) => Object.assign({ t: 'cone', p, s: [rTop, rBottom, h], m, c }, o || {});

// ------------------------------------------------------------------ LEVEL 6: THE NEST
function levelNest() {
  RNG = mulberry32(706);
  const P = [], lanterns = [], props = [], hides = [], crawlers = [], lights = [];
  const RX = 35, RZ = 30, CEIL = 25;
  const ell = (th, k = 1) => [Math.cos(th) * RX * k, Math.sin(th) * RZ * k];
  const tanYaw = (th) => Math.atan2(-RZ * Math.cos(th), -RX * Math.sin(th)) / DEG;
  const inward = (th) => { const nx = -Math.cos(th) / RX, nz = -Math.sin(th) / RZ, l = Math.hypot(nx, nz); return [nx / l, 0, nz / l]; };
  P.push(box([0, -0.5, 0], [RX * 2 + 8, 1, RZ * 2 + 8], 'rock', 0x5a544c));
  P.push(box([0, CEIL + 0.5, 0], [RX * 2 + 8, 1, RZ * 2 + 8], 'rock', 0x3a3632));
  // cavern wall: a ring of rock slabs, open to the east for the way out
  const N = 34, seg = 2 * Math.PI * 32.6 / N * 1.25;
  for (let k = 0; k < N; k++) {
    const th = k / N * Math.PI * 2;
    if (Math.abs(wrapAngle(th)) < 0.1) continue;
    const [x, z] = ell(th, 1.03);
    P.push(box([x, CEIL / 2, z], [seg, CEIL + 1, 2.4], 'rock', 0x4a4640, { r: [0, tanYaw(th), 0] }));
  }
  // east tunnel behind the rock door
  for (const s of [-1, 1]) P.push(box([39.5, 2.5, s * 2.2], [11, 5, 0.6], 'rock', 0x4a4640));
  P.push(box([39.5, 5.25, 0], [11, 0.5, 5], 'rock', 0x3a3632));
  P.push(box([44.8, 2.5, 0], [0.6, 5, 5], 'rock', 0x3a3632));
  // spawn ledge on the west wall and rock steps down
  P.push(box([-31, 5.5, 0], [7, 1, 9], 'rock', 0x6a645a));
  for (const [x, z, top] of [[-26, 1, 4.6], [-23.5, 2, 3.2], [-21, 1, 1.8]]) P.push(box([x, top / 2, z], [3, top, 3], 'rock', 0x5a544c));
  P.push(box([-31, 5.75, -5.8], [2, 0.5, 2], 'rock', 0x6a645a));
  // a ring of ledges along the north wall: the long quiet way round
  const ledges = [];
  for (let th = Math.PI + 0.25; th < Math.PI * 2 - 0.45; th += 0.16) {
    const [x, z] = ell(th, 0.955), y = 5 + Math.sin(th * 3) * 0.8;
    P.push(box([x, y - 0.25, z], [4.2, 0.5, 2.6], 'rock', 0x6a645a, { r: [0, tanYaw(th), 0] }));
    ledges.push([x, y, z]);
  }
  // old mining scaffolds against the south wall: the Warden can smash these
  ['s1', 's2', 's3'].forEach((id, i) => {
    const th = 1.2 + i * 0.65, [x, z] = ell(th, 0.9), yaw = tanYaw(th);
    P.push(box([x, 5.85, z], [5, 0.3, 2.6], 'wood', 0x6a5038, { r: [0, yaw, 0], slam: id }));
    for (const s of [-1, 1]) {
      const px = x + Math.cos(yaw * DEG) * s * 2.2, pz = z - Math.sin(yaw * DEG) * s * 2.2;
      P.push(cyl([px, 2.9, pz], 0.14, 5.8, 'wood', 0x4a3828, { slam: id }));
    }
  });
  // the nest: mattresses and cloth, broken chairs and tables, bones
  const gems = [[-6, 0.2, 4], [2, 0.2, -7], [5, 2.45, 6]];
  const nearGem = (x, z) => gems.some((g) => Math.hypot(g[0] - x, g[2] - z) < 2.4);
  for (let i = 0; i < 16; i++) {
    const a = i / 16 * Math.PI * 2 + rand(-0.2, 0.2), r = rand(6.5, 10.5), x = Math.cos(a) * r, z = Math.sin(a) * r;
    if (nearGem(x, z)) continue;
    P.push(box([x, 0.3, z], [rand(2, 3.4), 0.6, rand(1.4, 2.2)], 'cloth', pick([0x8a7a6a, 0x6a5a6a, 0x7a6a50, 0x5a6a6a]), { r: [rand(-6, 6), rand(0, 180), rand(-6, 6)], surf: 'STICKY' }));
  }
  for (let i = 0; i < 12; i++) {   // bones rattle: NOISY
    const a = rand(0, Math.PI * 2), r = rand(4, 11), x = Math.cos(a) * r, z = Math.sin(a) * r;
    if (nearGem(x, z)) continue;
    P.push(cyl([x, 0.13, z], 0.12, rand(1.4, 2.6), 'bone', 0xe0d4b8, { r: [90, rand(0, 180), 0], surf: 'NOISY' }));
  }
  for (let i = 0; i < 9; i++) {    // broken chairs and tables
    const a = rand(0, Math.PI * 2), r = rand(9, 13), x = Math.cos(a) * r, z = Math.sin(a) * r;
    P.push(box([x, 0.45, z], [1.1, 0.12, 1.1], 'wood', 0x6a4a30, { r: [rand(-25, 25), rand(0, 90), rand(-25, 25)] }));
    P.push(box([x + 0.3, 0.9, z - 0.3], [1.0, 1.0, 0.1], 'wood', 0x5a3a24, { r: [rand(-30, 30), rand(0, 90), 0] }));
  }
  P.push(box([5, 1.2, 6], [2.4, 2.4, 2.4], 'wood', 0x5a4030, { r: [0, 20, 0] }));    // a wardrobe on its side: a stone sits on top
  for (const [x, z, h] of [[-11, -14, 3.2], [13, -9, 2.6], [-13, 12, 3.6], [11, 15, 2.2]]) {
    P.push(box([x, h / 2, z], [2.2, h, 2.2], 'wood', 0x6a4a30, { r: [0, rand(0, 90), 0] }));
    P.push(box([x + 0.4, h + 0.6, z + 0.2], [1.6, 1.2, 1.6], 'cloth', 0x7a6a5a, { r: [rand(-10, 10), rand(0, 90), 0], surf: 'STICKY' }));
  }
  // stalagmites and stalactites
  for (let i = 0; i < 18; i++) {
    const a = rand(0, Math.PI * 2), k = rand(0.4, 0.85), x = Math.cos(a) * RX * k, z = Math.sin(a) * RZ * k;
    if (Math.hypot(x, z) < 12 || (x > 22 && Math.abs(z) < 5) || (x < -18 && Math.abs(z) < 6)) continue;
    const h = rand(3, 7.5);
    P.push(cone([x, h / 2, z], 0.06, rand(0.7, 1.3), h, 'rock', 0x6a645a));
  }
  for (let i = 0; i < 18; i++) {
    const a = rand(0, Math.PI * 2), k = rand(0.15, 0.85), x = Math.cos(a) * RX * k, z = Math.sin(a) * RZ * k, h = rand(4, 8.5);
    P.push(cone([x, CEIL - h / 2, z], rand(0.8, 1.5), 0.06, h, 'rock', 0x5a544c));
  }
  // the toy waits on top of a tall stalagmite
  P.push(cone([-14, 4, -12], 0.6, 2.2, 8, 'rock', 0x6a645a));
  P.push(box([-14, 8.1, -12], [1.4, 0.2, 1.4], 'rock', 0x6a645a));
  // glowing fungus
  for (let i = 0; i < 30; i++) {
    const th = rand(0, Math.PI * 2), [x, z] = ell(th, rand(0.85, 0.96));
    P.push(cone([x, 0.12, z], 0.02, rand(0.08, 0.2), 0.25, 'glow', pick([0x40c0a0, 0x50a0c0, 0x70d0b0]), { col: false }));
  }
  lights.push({ p: [-20, 3, -18], len: 0.05, color: 0x60ffc0, intensity: 1.4, distance: 12 }, { p: [20, 3, 18], len: 0.05, color: 0x60ffc0, intensity: 1.4, distance: 12 });
  // crawlers on the walls and the roof of the cave
  for (const [th, y] of [[0.6, 9], [2.2, 10], [3.9, 8], [4.8, 11]]) { const [x, z] = ell(th, 0.985); crawlers.push({ p: [x, y, z], n: inward(th) }); }
  crawlers.push({ p: [-10, CEIL - 0.1, -6], n: [0, -1, 0] }, { p: [9, CEIL - 0.1, 9], n: [0, -1, 0] });
  // things to throw and places to hide
  for (const p of [[-20, 0.3, 6], [-16, 0.3, -8], [10, 0.3, -16], [18, 0.3, 4], [-4, 0.3, -15]]) props.push({ type: 'stone', p });
  for (const p of [[-30, 6.3, 3], [16, 0.3, 12], [-22, 0.3, -12]]) props.push({ type: 'bottle', p });
  hides.push({ type: 'barrel', p: [-18, 0, 10] }, { type: 'barrel', p: [17, 0, -13] }, { type: 'wardrobe', p: [-12, 0, -20], yaw: 20 }, { type: 'crawlspace', p: [13, 0, 15], yaw: -30 });
  const mid = ledges[Math.floor(ledges.length / 2)];
  lanterns.push({ p: [-29.5, 6, -3], spawnDir: [1, 0, 0] }, { p: [mid[0], mid[1], mid[2]], spawnDir: [0, 0, 1] }, { p: [29, 0, 4], spawnDir: [-1, 0, 0] });
  const wp = [];
  for (let k = 0; k < 8; k++) { const a = k / 8 * Math.PI * 2; wp.push([Math.cos(a) * 24, 0, Math.sin(a) * 19]); }
  for (let k = 0; k < 4; k++) { const a = k / 4 * Math.PI * 2 + 0.4; wp.push([Math.cos(a) * 14, 0, Math.sin(a) * 13]); }
  return {
    name: 'THE NEST', subtitle: 'it sleeps', index: 6,
    objectiveText: 'Steal the 3 glowing stones from beside the sleeping giant. Do not wake it.',
    objective: { type: 'stones', need: 3 },
    fog: [0x05080a, 0.035], hemi: [0x405868, 0x0c1012, 0.85], sun: { color: 0x506070, intensity: 0.2, dir: [0.2, 1, 0.3] },
    ambientLight: 0.2,
    ambience: { drips: 2, drone: [32.7], creaks: 0.5, wind: 0.2, windCut: 200 }, music: { drone: 0.5 },
    spawn: { p: [-32, 6.8, 1], yaw: -Math.PI / 2 },
    prims: P, lights, lanterns, props, hides, crawlers,
    pickups: [...gems.map((p) => ({ type: 'gem', p })), { type: 'toy', p: [-14, 8.22, -12] }, { type: 'battery', p: [-28.5, 6.02, 3] }],
    notes: [{ id: 12, p: [-30.5, 6.3, 2.5] }, { id: 13, p: [14, 0.3, 18] }],
    exit: { type: 'rockdoor', p: [35, 0, 0], yaw: 90, w: 3.2, h: 4, trigger: { p: [40, 1.2, 0], h: [2.5, 2, 1.8] } },
    signs: [{ p: [-29, 7.2, 4.4], yaw: 180, w: 1.6, h: 0.9, text: 'THE NEST\nIt is asleep. Loud sounds and lights wake it - listen to its breathing. Cloth is quiet. Bones are not.' }],
    warden: { mode: 'sleep', startState: 'SLEEP', ground: 0, start: [0, 0, 0], startYaw: Math.PI / 2, waypoints: wp, hearing: 1.2, sight: 1.0, walkSpeed: 1.3, huntSpeed: 3.0, sightRange: 28, canCatch: true, searchTime: 20, reachSpeed: 2.4, breath: 1.2, shed: true },
    killY: -10,
  };
}

// ------------------------------------------------------------------ LEVEL 7: THE FLOODED CHAPEL
function levelChapel() {
  RNG = mulberry32(807);
  const P = [], props = [], lanterns = [], hides = [], crawlers = [];
  const ST = 0x6a665e, WD = 0x5a4030;
  // nave: floor (the Warden's ground, deep under the water), walls, roof
  P.push(box([0, -2.5, -5], [22, 1, 56], 'stone', 0x4a4a44));
  P.push(box([-9.5, 7, -5], [1, 18, 53], 'stone', ST)); P.push(box([9.5, 7, -5], [1, 18, 53], 'stone', ST));
  P.push(box([0, 7, -31], [20, 18, 1], 'stone', ST)); P.push(box([0, 7, 21], [20, 18, 1], 'stone', ST));
  P.push(box([0, 16.5, -1.25], [20, 1, 45.5], 'roof', 0x3a3434));
  P.push(box([-3.5, 16.5, -27.75], [13, 1, 7.5], 'roof', 0x3a3434));
  // moonlit windows
  for (const s of [-1, 1]) for (const z of [12, 2, -8, -18]) P.push(box([s * 8.96, 11, z], [0.05, 5, 1.6], 'glow', 0x5a6a7a, { col: false }));
  // the bell tower in the north-east corner
  P.push(box([3.3, 5, -27.25], [0.6, 14, 6.5], 'stone', ST)); P.push(box([3.3, 22, -27.25], [0.6, 15, 6.5], 'stone', ST));
  P.push(box([3.3, 13.25, -29.25], [0.6, 2.5, 2.5], 'stone', ST)); P.push(box([3.3, 13.25, -25], [0.6, 2.5, 2], 'stone', ST));
  P.push(box([6.25, 2.6, -24.3], [6.5, 9.2, 0.6], 'stone', ST)); P.push(box([6.25, 19.15, -24.3], [6.5, 20.7, 0.6], 'stone', ST));
  P.push(box([4.9, 8, -24.3], [3.8, 1.6, 0.6], 'stone', ST)); P.push(box([8.95, 8, -24.3], [1.1, 1.6, 0.6], 'stone', ST));
  P.push(box([9.5, 22.75, -27.75], [1, 13.5, 7.5], 'stone', ST)); P.push(box([6.5, 22.75, -31], [7, 13.5, 1], 'stone', ST));
  P.push(box([3.9, 29.75, -27.5], [1.8, 0.5, 7], 'roof', 0x3a3434)); P.push(box([7.85, 29.75, -27.5], [3.3, 0.5, 7], 'roof', 0x3a3434));
  P.push(box([5.5, 29.75, -29.6], [1.4, 0.5, 2.8], 'roof', 0x3a3434)); P.push(box([5.5, 29.75, -25.4], [1.4, 0.5, 2.8], 'roof', 0x3a3434));
  // tower landings every 3.5 m, ropes between them, the belfry
  P.push(box([5.1, 11.75, -27.55], [3, 0.5, 5.9], 'wood', WD)); P.push(box([7.7, 15.25, -27.55], [2.6, 0.5, 5.9], 'wood', WD));
  P.push(box([5.1, 18.75, -27.55], [3, 0.5, 5.9], 'wood', WD)); P.push(box([7.7, 22.25, -27.55], [2.6, 0.5, 5.9], 'wood', WD));
  P.push(box([7.2, 24.75, -27.55], [3.6, 0.5, 5.9], 'wood', WD)); P.push(box([4.5, 24.75, -26.3], [1.8, 0.5, 3.4], 'wood', WD));
  for (const [x, y, z, h] of [[6.5, 13.75, -26, 3.5], [6.5, 17.25, -29, 3.5], [6.5, 20.75, -26, 3.5], [5.2, 22.1, -29.2, 5.4], [5.5, 27.25, -26.6, 4.5]]) P.push(cyl([x, y, z], 0.06, h, 'rope', 0xa08a60, { surf: 'STICKY' }));
  P.push(box([7.6, 28.9, -27.5], [3.2, 0.3, 0.3], 'wood', WD));
  // narthex balcony (spawn) and drowned pews piled into stepping stones
  P.push(box([0, 3.5, 18.75], [18, 1, 3.5], 'stone', 0x7a766a));
  const piles = [[0, 14.5, 4.4], [-2.5, 10, 4.7], [2, 5.5, 5.0], [-2.5, 1, 5.3], [2.5, -3.5, 5.6], [-2, -8, 5.9], [2.5, -12.5, 6.2], [-2, -17, 6.5], [1, -21.5, 6.8]];
  for (const [x, z, top] of piles) {
    const yaw = rand(-20, 20);
    P.push(box([x, (top - 2) / 2, z], [3.2, top + 2, 2.4], 'wood', 0x4a3424, { r: [0, yaw, 0], block: false }));
    for (let k = 0; k < 2; k++) P.push(box([x + rand(-0.4, 0.4), top + 0.1 + k * 0.2, z + rand(-0.6, 0.6)], [3.4, 0.2, 0.55], 'wood', 0x6a4a30, { r: [rand(-4, 4), yaw + rand(-25, 25), 0], block: false }));
  }
  // pillars with capitals (a toy sits on one)
  for (const s of [-1, 1]) for (const z of [12, 4, -4, -12, -20]) {
    P.push(cyl([s * 5, 6, z], 0.8, 16, 'stone', 0x7a766a));
    P.push(box([s * 5, 14.2, z], [1.9, 0.4, 1.9], 'stone', 0x8a8478));
  }
  // side galleries with railings
  for (const s of [-1, 1]) {
    P.push(box([s * 8, 5.75, -5], [2, 0.5, 38], 'wood', 0x5a4030));
    P.push(cyl([s * 7.05, 6.65, -5], 0.04, 38, 'metal', 0x3a3632, { r: [90, 0, 0] }));
    for (let z = -23; z <= 13; z += 3) P.push(cyl([s * 7.05, 6.3, z], 0.04, 0.7, 'metal', 0x3a3632));
  }
  // the organ: a case, NOISY pipes up to the loft, the loft, and a beam bridge to the tower window
  P.push(box([-6, 1, -24.8], [6, 6, 0.6], 'wood', 0x3a2818));
  for (let i = 0; i < 12; i++) {
    const top = 10.4 + 2.2 * Math.pow(Math.sin(i * 0.52), 2);
    P.push(cyl([-8.5 + i * 0.45, (4 + top) / 2, -24.7], 0.17, top - 4, 'metal', 0xa89060, { surf: 'NOISY' }));
  }
  P.push(box([-6, 9.75, -27.5], [6, 0.5, 6], 'wood', 0x5a4030));
  for (const x of [-8.5, -3.5]) P.push(cyl([x, 3.75, -30], 0.3, 11.5, 'stone', 0x6a665e));
  P.push(boxBetween([-3.2, 10.12, -27.3], [3.3, 12.05, -27.3], 0.6, 0.22, 'wood', 0x5a4030, { slam: 'beam' }));
  // crawlers high on the walls and the roof
  crawlers.push({ p: [-8.9, 12, -5], n: [1, 0, 0] }, { p: [8.9, 13, 8], n: [-1, 0, 0] }, { p: [0, 15.9, -12], n: [0, -1, 0] });
  props.push({ type: 'bottle', p: [-8, 6.3, -12] }, { type: 'bottle', p: [8, 6.3, 2] }, { type: 'bottle', p: [0, 4.8, 14.5] }, { type: 'bottle', p: [-6, 10.3, -28] }, { type: 'stone', p: [8, 6.3, -16] }, { type: 'can', p: [-8, 6.3, 10] });
  hides.push({ type: 'wardrobe', p: [8.4, 6.0, -8], yaw: -90 }, { type: 'barrel', p: [-8, 6.0, 6] });
  lanterns.push({ p: [-6, 4.0, 19], spawnDir: [1, 0, -1] }, { p: [-8, 6.0, 0], spawnDir: [0, 0, -1] }, { p: [-7.5, 10, -28.5], spawnDir: [1, 0, 0] }, { p: [5, 19, -29.5], spawnDir: [0, 0, 1] });
  const wp = [[0, 0, 16], [0, 0, 10], [0, 0, 4], [0, 0, -2], [0, 0, -8], [0, 0, -14], [0, 0, -20], [-2, 0, -21]];
  return {
    name: 'THE FLOODED CHAPEL', subtitle: 'it wades', index: 7,
    objectiveText: 'Climb the bell tower and ring the chapel bell. The water rises every minute.',
    objective: { type: 'chapelbell', need: 1 },
    fog: [0x0e1414, 0.035], hemi: [0x506878, 0x101818, 1.1], sun: { color: 0x8090b0, intensity: 0.4, dir: [0.4, 1, 0.3] },
    ambientLight: 0.3,
    ambience: { drips: 2.5, water: 0.6, drone: [43.65], creaks: 0.6, wind: 0.2, windCut: 300 }, music: { drone: 0.6 },
    spawn: { p: [0, 4.8, 18.5], yaw: 0 },
    prims: P, props, lanterns, hides, crawlers, lights: [{ p: [0, 15.8, 0], len: 1.5, color: 0xb0c0d0, intensity: 2, distance: 18, flicker: true }],
    pickups: [{ type: 'toy', p: [5, 14.45, 4] }, { type: 'battery', p: [8, 6.02, -4] }, { type: 'battery', p: [7.8, 15.52, -28] }],
    bells: [{ p: [7.6, 28.75, -27.5], len: 1.3, kind: 'chapelbell', size: 1.6 }],
    notes: [{ id: 14, p: [3, 4.3, 19.5] }, { id: 15, p: [-7, 10.3, -29.5] }],
    water: { level: 3.0, max: 9.0, finalMax: 14, area: [-9, -30.5, 9, 20.5] },
    peeks: [{ eye: [7.6, 8.0, -23.6], look: [6.5, 13, -27.5] }],
    exit: { type: 'grate', p: [5.5, 29.9, -27.5], trigger: { p: [5.5, 31.2, -27.5], h: [1.5, 1.0, 1.5] } },
    signs: [{ p: [2.6, 5.0, 17.2], yaw: 0, w: 1.6, h: 0.9, text: 'THE FLOODED CHAPEL\nThe water rises every minute. It is slow and slippery. Climb. The bell is at the top of the tower.' }],
    warden: { mode: 'normal', ground: -2, waypoints: wp, start: [0, 0, -20], hearing: 1.0, sight: 1.0, walkSpeed: 1.0, huntSpeed: 2.4, sightRange: 30, canCatch: true, searchTime: 22, reachSpeed: 2.3, breath: 1.1, shed: true },
    killY: -20,
  };
}

// ------------------------------------------------------------------ LEVEL 8: THE HEART
function levelHeart() {
  RNG = mulberry32(908);
  const P = [], props = [], lanterns = [], crawlers = [];
  const F = 0xa04048, FD = 0x7a2a34, BONE = 0xd8c8b0, R = 26;
  // the chamber: a ring of breathing flesh around the heart
  P.push(box([0, -0.5, -6.5], [58, 1, 41], 'flesh', FD, { surf: 'STICKY' }));      // floor (a chasm cuts across the south)
  P.push(box([0, -0.5, 24], [12, 1, 4], 'flesh', FD, { surf: 'STICKY' }));
  const N = 30, segW = 2 * Math.PI * R / N * 1.2;
  for (let k = 0; k < N; k++) {
    const th = k / N * Math.PI * 2;
    if (Math.abs(th - Math.PI / 2) < 0.12) continue;
    P.push(box([Math.cos(th) * (R + 0.6), 15, Math.sin(th) * (R + 0.6)], [segW, 32, 1.2], 'flesh', F, { r: [0, (-th - Math.PI / 2) / DEG, 0], surf: 'STICKY' }));
  }
  // ceiling, with a plug over the shaft that falls away at the end
  P.push(box([-7.75, 31.5, 0], [40.5, 1, 58], 'flesh', FD)); P.push(box([24.75, 31.5, 0], [6.5, 1, 58], 'flesh', FD));
  P.push(box([17, 31.5, -16.75], [9, 1, 24.5], 'flesh', FD)); P.push(box([17, 31.5, 16.75], [9, 1, 24.5], 'flesh', FD));
  P.push(box([17, 31.5, 0], [9, 1.2, 9], 'flesh', FD, { stage: 'final' }));
  // entrance tunnel (south)
  for (const s of [-1, 1]) P.push(box([s * 2.3, 2.5, 29], [0.6, 5, 6.4], 'flesh', F, { surf: 'STICKY' }));
  P.push(box([0, 5.25, 29], [5.2, 0.5, 6.4], 'flesh', FD)); P.push(box([0, -0.5, 29], [5.2, 1, 6.4], 'flesh', FD, { surf: 'STICKY' }));
  P.push(box([0, 2.5, 32.4], [5.2, 5, 0.6], 'flesh', FD));
  // the bridge over the chasm (collapses after the first cord)
  P.push(box([0, -0.25, 18], [3, 0.5, 8.2], 'flesh', F, { surf: 'STICKY', stage: 'a' }));
  // the heart's solid core (the beating mesh is built by the Heart system)
  P.push(cyl([0, 9, 0], 4.8, 11, 'flesh', 0x902030, { surf: 'STICKY' }));
  // rib arches overhead
  for (const z of [-18, -9, 9]) {
    let prev = null;
    for (let i = 0; i <= 10; i++) {
      const a = Math.PI * (0.12 + 0.76 * i / 10), pt = [Math.cos(a) * 23, 2 + Math.sin(a) * 23, z];
      if (prev) P.push(cylBetween(prev, pt, 0.35, 'bone', BONE, { surf: 'STICKY' }));
      prev = pt;
    }
    for (const s of [-1, 1]) P.push(cylBetween([s * 21.3, 10.6, z], [s * 23.2, -0.2, z], 0.45, 'bone', BONE, { surf: 'STICKY' }));
  }
  // west: polyps up to the platform of the first cord (they rot away after the second)
  for (const [x, z, top] of [[-12, 4, 1.5], [-15, 5.5, 3], [-17.8, 4.5, 4]]) P.push(box([x, top / 2, z], [2.8, top, 2.8], 'flesh', F, { surf: 'STICKY', stage: 'b' }));
  P.push(box([-21, 4.75, 0], [6, 0.5, 6], 'flesh', F, { surf: 'STICKY', stage: 'b' }));
  P.push(box([-25, 9.75, -6], [2.2, 0.5, 2.2], 'flesh', F, { surf: 'STICKY' }));   // the toy's alcove
  // after cord A: a stair of rib-flesh rises to the north platform
  for (let i = 0; i <= 8; i++) {
    const t = i / 8, x = lerp(-19, -3, t), z = lerp(-3, -16, t), top = 6 + t * 7;
    P.push(box([x, top - 0.25, z], [2.6, 0.5, 2.6], 'flesh', F, { surf: 'STICKY', stage: 'a', reveal: true }));
  }
  P.push(box([0, 13.75, -19], [8, 0.5, 5], 'flesh', F, { surf: 'STICKY', stage: 'a2', reveal: true }));
  // after cord B: another stair climbs east to the platform under the shaft
  for (let i = 0; i <= 7; i++) {
    const t = i / 7, x = lerp(4, 13, t), z = lerp(-17, -5.2, t), top = 14.7 + t * 4.6;
    P.push(box([x, top - 0.25, z], [2.6, 0.5, 2.6], 'flesh', F, { surf: 'STICKY', stage: 'b', reveal: true }));
  }
  P.push(box([17, 19.75, 0], [8, 0.5, 8], 'flesh', F, { surf: 'STICKY', stage: 'b2', reveal: true }));
  // after the last cord: tendrils grow up into the shaft
  for (let k = 0; k < 5; k++) {
    const a = k / 5 * Math.PI * 2;
    P.push(cylBetween([17 + Math.cos(a) * 3.2, 20, Math.sin(a) * 3.2], [17 + Math.cos(a + 0.7) * 2.6, 33, Math.sin(a + 0.7) * 2.6], 0.3, 'flesh', F, { surf: 'STICKY', stage: 'final', reveal: true }));
  }
  // the shaft to daylight: flesh giving way to rock, moss and roots
  const SX = 17, SR = 4.6, SN = 14;
  for (let b = 0; b < 6; b++) {
    const y0 = 32 + b * 7.4;
    for (let k = 0; k < SN; k++) {
      const th = (k + (b % 2) * 0.5) / SN * Math.PI * 2, r = RNG();
      const [m, c, surf] = b < 2 ? ['flesh', F, 'STICKY'] : r < 0.55 ? ['rock', 0x6a645a, 'DEFAULT'] : ['moss', 0x6a8a5a, 'STICKY'];
      P.push(box([SX + Math.cos(th) * (SR + 0.5), y0 + 3.7, Math.sin(th) * (SR + 0.5)], [2 * Math.PI * SR / SN * 1.2, 7.4, 1], m, c, { r: [0, (-th - Math.PI / 2) / DEG, 0], surf }));
    }
    const th = b * 2.1;
    P.push(box([SX + Math.cos(th) * 3.6, y0 + 3.5, Math.sin(th) * 3.6], [2.2, 0.3, 1.4], 'rock', 0x7a746a, { r: [0, (-th - Math.PI / 2) / DEG, 0] }));
  }
  for (let i = 0; i < 12; i++) {
    const th = RNG() * Math.PI * 2, y = 34 + RNG() * 38;
    P.push(cylBetween([SX + Math.cos(th) * SR, y, Math.sin(th) * SR], [SX + Math.cos(th + 0.4) * 2.8, y - 2.2, Math.sin(th + 0.4) * 2.8], 0.1, 'bark', 0x4a3a2a, { surf: 'STICKY' }));
  }
  // the meadow at the top (dark until the sun comes up)
  P.push(box([-10.3, 75.5, 0], [45.4, 1, 100], 'grass', 0x5a6a3a)); P.push(box([44.3, 75.5, 0], [45.4, 1, 100], 'grass', 0x5a6a3a));
  P.push(box([17, 75.5, -27.3], [9.2, 1, 45.4], 'grass', 0x5a6a3a)); P.push(box([17, 75.5, 27.3], [9.2, 1, 45.4], 'grass', 0x5a6a3a));
  for (let i = 0; i < 14; i++) {
    const a = RNG() * Math.PI * 2, r = 12 + RNG() * 30, x = SX + Math.cos(a) * r, z = Math.sin(a) * r, h = 4 + RNG() * 4;
    P.push(cyl([x, 76 + h / 2, z], 0.3, h, 'bark', 0x5a4a3a));
    P.push(cone([x, 76 + h + 2, z], 0.1, 2.4, 5, 'moss', 0x4a7a3a, { col: false }));
  }
  for (const [th, y] of [[0.4, 9], [1.3, 12], [2.6, 10], [3.6, 8], [4.6, 11]]) crawlers.push({ p: [Math.cos(th) * (R - 0.3), y, Math.sin(th) * (R - 0.3)], n: [-Math.cos(th), 0, -Math.sin(th)] });
  crawlers.push({ p: [-8, 30.9, 8], n: [0, -1, 0] });
  for (const p of [[-6, 0.3, 10], [8, 0.3, 11], [-15, 0.3, -6], [14, 0.3, -12]]) props.push({ type: 'stone', p });
  lanterns.push({ p: [1.2, 0, 27.5], spawnDir: [0, 0, -1] }, { p: [-12, 0, 8], spawnDir: [1, 0, 0] }, { p: [2.5, 14, -20], spawnDir: [0, 0, 1], stage: 'a2' }, { p: [19.5, 20, 2.5], spawnDir: [-1, 0, 0], stage: 'b2' });
  const wp = [];
  for (let k = 0; k < 8; k++) { const a = k / 8 * Math.PI * 2; wp.push([Math.cos(a) * 15, 0, Math.sin(a) * 15]); }
  return {
    name: 'THE HEART', subtitle: 'let him go', index: 8,
    objectiveText: 'Grip the knots and pull hard. Cut the 3 cords.',
    objective: { type: 'cord', need: 3 },
    fog: [0x200606, 0.03], hemi: [0x803030, 0x200808, 0.9], sun: { color: 0x802020, intensity: 0.3, dir: [0.5, 0.6, -0.3] },
    ambientLight: 0.35,
    ambience: { drone: [32.7, 49], wet: 1.5, drips: 1 }, music: { drone: 0.5 },
    spawn: { p: [0, 1.0, 29], yaw: 0 },
    prims: P, props, lanterns, crawlers, lights: [],
    pickups: [{ type: 'toy', p: [-24.7, 10.05, -6] }, { type: 'battery', p: [-1, 0.02, 27] }, { type: 'battery', p: [-20, 5.02, 2] }],
    notes: [{ id: 16, p: [-1.2, 0.3, 28.6] }, { id: 17, p: [-12.5, 0.3, -12] }],
    hides: [{ type: 'pod', p: [-10, 0, 12] }, { type: 'pod', p: [12, 0, 9] }],
    heart: { p: [0, 9, 0], r: 6 },
    cords: [
      { a: [-25.8, 6.2, 0], handle: [-20.5, 5.9, 0.5], b: [-5.5, 9, 0], opens: 'a' },
      { a: [0, 17, -25.8], handle: [0, 14.9, -21], b: [0, 12, -5], stage: 'a', locked: true, opens: 'b' },
      { a: [25.6, 24, 0], handle: [21.2, 20.9, 0.5], b: [5, 13, 0], stage: 'b', locked: true },
    ],
    stageCollapse: { b: ['a'], final: ['b'] }, stageLinks: { a: ['a2'], b: ['b2'] },
    fallToward: [9, 0, -10], trueEnding: true,
    exit: { type: 'rim', p: [SX, 76, 0], trigger: { p: [SX, 77.2, 0], h: [6, 1.2, 6] } },
    signs: [{ p: [1.9, 1.6, 27], yaw: -90, w: 1.4, h: 0.9, text: 'THE HEART\nGrip a swollen knot on a cord and PULL HARD until it snaps. Three cords hold it shut.' }],
    warden: { mode: 'normal', ground: 0, waypoints: wp, start: [0, 0, -15], hearing: 1.2, sight: 1.1, walkSpeed: 1.4, huntSpeed: 3.2, sightRange: 32, canCatch: true, searchTime: 20, reachSpeed: 2.6, breath: 1.3, shed: true },
    killY: -8,
  };
}

// ------------------------------------------------------------------ ENDLESS DESCENT: seeded chunks joined by doorways
// Every floor is generated from (seed, floor), built from the same prims (merged per material),
// and disposed when you drop into the pit to the next floor.
function levelEndless() {
  const floor = Game.endless.floor, seed = Game.endless.seed;
  RNG = mulberry32(seed * 7919 + floor * 104729);
  const P = [], lanterns = [], pickups = [], props = [], hides = [], crawlerSpots = [], lights = [], pits = [];
  const themes = [['concrete', 0x6a6a62, 'rust', 0x7a5a48], ['brick', 0x7a5a4a, 'metal', 0x6a6a70], ['rock', 0x5a544c, 'moss', 0x6a8a5a], ['flesh', 0x8a3a40, 'bone', 0xd0c0a8]];
  const [WM, WC2, AM, AC] = themes[Math.min(themes.length - 1, Math.floor((floor - 1) / 3))];
  const DW = 1.2, DH = 2.8;
  // a wall across the corridor at z with a doorway at x = 0 (door = false: solid)
  const endWall = (y, z, W, H, door = true) => {
    const L = -W / 2 - 1, Rr = W / 2 + 1;
    if (!door) { P.push(box([0, y + H / 2, z], [Rr - L, H, 0.6], WM, WC2)); return; }
    const dh = Math.min(DH, H);
    P.push(box([(L - DW) / 2, y + H / 2, z], [-DW - L, H, 0.6], WM, WC2));
    P.push(box([(DW + Rr) / 2, y + H / 2, z], [Rr - DW, H, 0.6], WM, WC2));
    if (H > dh) P.push(box([0, y + dh + (H - dh) / 2, z], [DW * 2, H - dh, 0.6], WM, WC2));
  };
  const shell = (y, z0, W, H, L, opts = {}) => {
    const zc = z0 - L / 2;
    if (!opts.noFloor) P.push(box([0, y - 0.5, zc], [W + 2, 1, L], WM, WC2));
    P.push(box([0, y + H + 0.5, zc], [W + 2, 1, L], WM, WC2));
    P.push(box([-W / 2 - 0.5, y + H / 2, zc], [1, H, L], WM, WC2));
    P.push(box([W / 2 + 0.5, y + H / 2, zc], [1, H, L], WM, WC2));
    endWall(y, z0, W, H, opts.doorIn !== false);
    endWall(y, z0 - L, W, H, opts.doorOut !== false);
  };
  let y = 0, z = 0, wp = [], wStart = null, wGround = 0, spawn = null;
  const middle = 3 + Math.min(floor, 5);
  const seq = ['start'];
  const cavernAt = 1 + Math.floor(RNG() * middle);
  for (let i = 1; i <= middle; i++) seq.push(i === cavernAt ? 'cavern' : pick(['tunnel', 'room', 'bridge', 'vents', 'shaft']));
  seq.push('end');
  for (const type of seq) {
    if (type === 'start') {
      shell(y, z, 8, 4, 8, { doorIn: false });
      spawn = [0, y + 0.8, z - 1.6];
      lanterns.push({ p: [2.6, y, z - 2.5], spawnDir: [-1, 0, -1] });
      if (RNG() < 0.6) pickups.push({ type: 'battery', p: [-2.8, y + 0.02, z - 6] });
      lights.push({ p: [0, y + 4, z - 4], len: 0.5, color: 0xffc890, intensity: 2, distance: 9, flicker: true });
      z -= 8;
    } else if (type === 'tunnel') {
      const L = 12 + Math.floor(RNG() * 5);
      shell(y, z, 3.2, 3, L);
      P.push(cyl([-1.25, y + 2.4, z - L / 2], 0.15, L, AM, AC, { r: [90, 0, 0] }));
      for (let i = 0; i < 3; i++) P.push(box([rand(-1, 1), y + 0.15, z - rand(2, L - 2)], [rand(0.3, 0.6), 0.3, rand(0.3, 0.6)], WM, WC2, { r: [0, rand(0, 90), 0] }));
      props.push({ type: pick(['stone', 'can', 'bottle']), p: [rand(-1, 1), y + 0.3, z - rand(2, L - 2)] });
      crawlerSpots.push({ p: [0, y + 2.95, z - L / 2], n: [0, -1, 0] });
      z -= L;
    } else if (type === 'room') {
      shell(y, z, 10, 5, 10);
      for (let i = 0; i < 5; i++) { const s = rand(0.9, 1.5); P.push(box([rand(-4, 4), y + s / 2, z - rand(1.5, 8.5)], [s, s, s], 'wood', 0x8a6a48, { inst: 'crate' })); }
      if (RNG() < 0.7) hides.push({ type: RNG() < 0.5 ? 'locker' : 'barrel', p: [4.3, y, z - 5], yaw: -90 });
      props.push({ type: 'bottle', p: [rand(-3, 3), y + 0.3, z - rand(2, 8)] }, { type: 'stone', p: [rand(-3, 3), y + 0.3, z - rand(2, 8)] });
      if (RNG() < 0.35) pickups.push({ type: 'battery', p: [-4, y + 0.02, z - 8.5] });
      if (RNG() < 0.25) props.push({ type: 'flare', p: [-3.5, y + 0.3, z - 2] });
      crawlerSpots.push({ p: [-4.9, y + 3, z - 5], n: [1, 0, 0] });
      lights.push({ p: [0, y + 5, z - 5], len: 1, color: 0xffd0a0, intensity: 2.2, distance: 10, flicker: RNG() < 0.5 });
      z -= 10;
    } else if (type === 'bridge') {   // a bottomless gap crossed on a plank
      const L = 14;
      shell(y, z, 10, 6, L, { noFloor: true });
      P.push(box([0, y - 0.5, z - 1.25], [12, 1, 2.5], WM, WC2)); P.push(box([0, y - 0.5, z - L + 1.25], [12, 1, 2.5], WM, WC2));
      const broken = RNG() < 0.5;
      if (broken) { P.push(box([0, y - 0.1, z - 4.6], [0.8, 0.15, 4.2], 'wood', 0x6a5038)); P.push(box([0, y - 0.1, z - 10.1], [0.8, 0.15, 3.8], 'wood', 0x6a5038)); }
      else P.push(box([0, y - 0.1, z - L / 2], [0.8, 0.15, L - 5], 'wood', 0x6a5038));
      P.push(cyl([-4.6, y + 1.5, z - L / 2], 0.1, L, AM, AC, { r: [90, 0, 0] })); P.push(cyl([4.6, y + 1.5, z - L / 2], 0.1, L, AM, AC, { r: [90, 0, 0] }));
      crawlerSpots.push({ p: [4.9, y + 3, z - L / 2], n: [-1, 0, 0] });
      z -= L;
    } else if (type === 'vents') {   // a low duct maze: Crawlers love it
      const L = 14, W = 6, H = 1.3;
      shell(y, z, W, H, L);
      for (const x of [-1, 1]) {   // two lane walls, each with one gap to cross through
        const gapAt = rand(3, L - 3);
        P.push(box([x, y + H / 2, z - (gapAt - 0.8) / 2], [0.15, H, gapAt - 0.8], 'metal', 0x6a7068));
        P.push(box([x, y + H / 2, z - (gapAt + 0.8 + L) / 2], [0.15, H, L - gapAt - 0.8], 'metal', 0x6a7068));
      }
      props.push({ type: 'can', p: [2, y + 0.3, z - 7] });
      crawlerSpots.push({ p: [-2, y + 0.2, z - 7], n: [0, 1, 0] });
      z -= L;
    } else if (type === 'shaft') {   // drop 8 m down a square shaft
      const D = 8, W = 5, L = 5, zc = z - L / 2;
      P.push(box([0, y - 0.5, z - 1], [W + 2, 1, 2], WM, WC2));                         // lip to step off
      P.push(box([0, y - D - 0.5, zc], [W + 2, 1, L], WM, WC2));                        // bottom
      P.push(box([0, y + 3.5, zc], [W + 2, 1, L], WM, WC2));                            // ceiling
      P.push(box([-W / 2 - 0.5, y - D / 2 + 1.5, zc], [1, D + 3, L], WM, WC2)); P.push(box([W / 2 + 0.5, y - D / 2 + 1.5, zc], [1, D + 3, L], WM, WC2));
      endWall(y, z, W, 3); P.push(box([0, y - D / 2, z], [W + 2, D, 0.6], WM, WC2));
      endWall(y - D, z - L, W, 3); P.push(box([0, y - 0.75, z - L], [W + 2, 8.5, 0.6], WM, WC2));
      P.push(cyl([-1.8, y - D / 2, zc - 1], 0.08, D, AM, AC)); P.push(cyl([1.8, y - D / 2, zc + 1], 0.08, D, AM, AC));
      for (let k = 1; k < 3; k++) P.push(box([k % 2 ? -1.5 : 1.5, y - k * 2.7, zc], [1.6, 0.25, 1.4], WM, WC2));
      y -= D; z -= L;
    } else if (type === 'cavern') {  // the Warden's room: it cannot fit through the doors
      const W = 28, H = 18, L = 28, zc = z - L / 2;
      shell(y, z, W, H, L);
      for (let i = 0; i < 6; i++) { const h = rand(3, 7); P.push(cone([rand(-11, 11), y + h / 2, zc + rand(-9, 9)], 0.08, rand(0.8, 1.5), h, 'rock', 0x6a645a)); }
      for (let i = 0; i < 4; i++) P.push(box([rand(-10, 10), y + 0.4, zc + rand(-10, 10)], [rand(1, 2), 0.8, rand(1, 2)], 'rock', 0x5a544c));
      for (let k = 0; k < 6; k++) P.push(box([-12.5, y + 3.5 + k * 0.6, z - 3 - k * 4], [3, 0.4, 3], WM, WC2));   // a ledge route along the west wall
      hides.push({ type: 'barrel', p: [12.5, y, zc + 6] }, { type: 'locker', p: [13.4, y, zc - 6], yaw: -90 });
      props.push({ type: 'bottle', p: [6, y + 0.3, z - 4] }, { type: 'stone', p: [-6, y + 0.3, z - 10] }, { type: 'stone', p: [8, y + 0.3, z - 20] });
      wp = [[-8, 0, zc - 8], [8, 0, zc - 8], [8, 0, zc + 8], [-8, 0, zc + 8], [0, 0, zc]];
      wStart = [0, 0, zc - 8]; wGround = y;
      crawlerSpots.push({ p: [10, y + H - 0.1, zc], n: [0, -1, 0] }, { p: [-13.9, y + 8, zc + 4], n: [1, 0, 0] });
      lights.push({ p: [0, y + H, zc], len: 3, color: 0xff9060, intensity: 3, distance: 22, flicker: true });
      z -= L;
    } else if (type === 'end') {
      shell(y, z, 8, 4, 8, { doorOut: false, noFloor: true });
      const pz = z - 5, h = 1.3;   // the floor leaves a real hole for the pit
      P.push(box([0, y - 0.5, (z + pz + h) / 2], [10, 1, z - pz - h], WM, WC2));
      P.push(box([0, y - 0.5, (pz - h + z - 8) / 2], [10, 1, pz - h - (z - 8)], WM, WC2));
      for (const sx of [-1, 1]) P.push(box([sx * (h + 5) / 2, y - 0.5, pz], [5 - h, 1, 2 * h], WM, WC2));
      pits.push({ type: 'pit', p: [0, y, pz], r: h, trigger: { p: [0, y + 0.2, pz], h: [1.0, 0.7, 1.0] } });
      z -= 8;
    }
  }
  const nC = Math.min(U1.CRAWLER_MAX - U1.CRAWLER_SHED_ON_HUNT, U1.ENDLESS_BASE_CRAWLERS + U1.ENDLESS_CRAWLERS_PER_FLOOR * (floor - 1));
  const crawlers = [];
  for (let i = 0; i < nC && crawlerSpots.length; i++) crawlers.push(crawlerSpots.splice(Math.floor(RNG() * crawlerSpots.length), 1)[0]);
  const depth = Math.min(1, floor / 12);
  return {
    name: `FLOOR ${floor}`, subtitle: 'endless descent', index: 9,
    objectiveText: 'Find the pit and go deeper. If it catches you, the run is over.',
    objective: { type: 'descend', need: 1 },
    fog: [new THREE.Color(0x14100e).lerp(new THREE.Color(0x200608), depth).getHex(), 0.05], hemi: [0x5a5048, 0x141010, 1.0 - depth * 0.3], sun: null,
    ambientLight: 0.25,
    ambience: { drips: 1.5, drone: [36.7 - floor * 0.5], creaks: 1, wet: WM === 'flesh' ? 1 : 0 }, music: { drone: 0.5 },
    spawn: { p: spawn, yaw: 0 },
    prims: P, lanterns, pickups, props, hides, crawlers, lights, pits,
    signs: [{ p: [-3.0, 1.6, -7.6], yaw: 0, w: 1.4, h: 0.8, text: `FLOOR ${floor}\nFind the pit at the far end. Best: ${Game.progress.endless.best} floors.` }],
    warden: { mode: 'normal', ground: wGround, waypoints: wp, start: wStart, hearing: 1.0, sight: 1.0, walkSpeed: 1.3, huntSpeed: 3.0, sightRange: 26, canCatch: true, searchTime: 18, reachSpeed: 2.4, breath: 1 },
    killY: y - 30,
  };
}

const LEVELS = [levelPlayground, levelDrains, levelCanopy, levelMill, levelWell, levelEscape, levelNest, levelChapel, levelHeart, levelEndless];
const LEVEL_NAMES = ['THE PLAYGROUND', 'THE DRAINS', 'THE CANOPY', 'THE MILL', 'THE WELL', 'THE ESCAPE', 'THE NEST', 'THE FLOODED CHAPEL', 'THE HEART', 'ENDLESS DESCENT'];

```

## PATCH #86 — 10. LEVEL LOADER / DISPOSER: stage groups (paths that rise / collapse), light refs for the sunrise

INSERT AFTER:
```js
const Level = {
  root: null, data: null, index: -1, roofs: new Map(), scene: null, envLights: [],

```
NEW CODE:
```js
  stages: new Map(), hemi: null, sun: null,   // UPDATE 1: stage groups (paths that rise / collapse), light refs for the sunrise
```

## PATCH #87 — 10. LEVEL LOADER / DISPOSER: systems

INSERT AFTER:
```js
    this.roofs.clear();
    AudioSys.stopAmbience();
  },
```
NEW CODE:
```js
    // UPDATE 1 systems
    this.stages.clear();
    Crawlers.clear(); Grab.clear(); Hiding.clear(); Notes.hide(); Water.restoreFog(); Subtitles.clear();
    Heart.active = false; FLESH_UNIFORMS.uPulse.value = 0; Crack.t = -1; Crack.mesh = null; Cords.list.length = 0; Cords.mesh = null;
    for (const h of Player.hands) { h.holding = null; h.cord = null; h.cling = null; }
```

## PATCH #88 — 10. LEVEL LOADER / DISPOSER: edit: this.root.add(hemi); this.hemi = hemi; this.sun = null;

FIND:
```js
    scene.background = new THREE.Color(data.fog[0]);
    const hemi = new THREE.HemisphereLight(data.hemi[0], data.hemi[1], data.hemi[2] * CONFIG.LIGHT_SCALE);
    this.root.add(hemi);
    if (data.sun) {
      const sun = new THREE.DirectionalLight(data.sun.color, data.sun.intensity * CONFIG.LIGHT_SCALE);
      sun.position.fromArray(data.sun.dir).normalize().multiplyScalar(60);
      this.root.add(sun);
    }
```
REPLACE WITH:
```js
    scene.background = new THREE.Color(data.fog[0]);
    const hemi = new THREE.HemisphereLight(data.hemi[0], data.hemi[1], data.hemi[2] * CONFIG.LIGHT_SCALE);
    this.root.add(hemi); this.hemi = hemi; this.sun = null;
    if (data.sun) {
      const sun = new THREE.DirectionalLight(data.sun.color, data.sun.intensity * CONFIG.LIGHT_SCALE);
      sun.position.fromArray(data.sun.dir).normalize().multiplyScalar(60);
      this.root.add(sun); this.sun = sun;
    }
```

## PATCH #89 — 10. LEVEL LOADER / DISPOSER: Nightmare keeps only half the lanterns and no batteries

FIND:
```js
    // interactables
    for (const d of data.lights || []) Interact.lamps.push(Interact.add(new SwingLamp(d)));
    for (const d of data.lanterns || []) Interact.lanterns.push(Interact.add(new Lantern(d)));
    for (const d of data.pickups || []) Interact.add(new Pickup(d));
    for (const d of data.valves || []) Interact.valves.push(Interact.add(new Valve(d)));
```
REPLACE WITH:
```js
    // interactables
    for (const d of data.lights || []) Interact.lamps.push(Interact.add(new SwingLamp(d)));
    // UPDATE 1: Nightmare keeps only half the lanterns and no batteries
    const nm = Game.mode === 'nightmare';
    (data.lanterns || []).forEach((d, i) => { if (!nm || d.objective || i % 2 === 0) Interact.lanterns.push(Interact.add(new Lantern(d))); });
    for (const d of data.pickups || []) if (!(nm && d.type === 'battery')) Interact.add(new Pickup(d));
    for (const d of data.valves || []) Interact.valves.push(Interact.add(new Valve(d)));
```

## PATCH #90 — 10. LEVEL LOADER / DISPOSER: content

FIND:
```js
    for (const d of data.signs || []) makeSign(d);
    for (const d of data.decals || []) makeHandprint(d);
    Warden.setupLevel(data);
    if (Game.colliderDebug) World.buildDebug(this.root);
```
REPLACE WITH:
```js
    for (const d of data.signs || []) makeSign(d);
    for (const d of data.decals || []) makeHandprint(d);
    // UPDATE 1 content
    for (const d of data.pits || []) Interact.add(new Exit(d));
    for (const d of data.hides || []) Hiding.add(d);
    for (const d of data.notes || []) Interact.add(new Note(d));
    Grab.setupLevel(data);
    Water.setupLevel(data);
    Cords.setupLevel(data);
    Heart.setupLevel(data);
    Hub.build(data);
    Warden.setupLevel(data);
    Crawlers.setupLevel(data);
    if (Game.colliderDebug) World.buildDebug(this.root);
```

## PATCH #91 — 10. LEVEL LOADER / DISPOSER: stage / slam groups

INSERT AFTER:
```js
    const wg = (data.warden && data.warden.ground) || 0;
    const buckets = new Map(), inst = new Map(), roofGeos = new Map(), roofCols = new Map(), planes = { water: [], mist: [] };
    for (const prim of data.prims) {
```
NEW CODE:
```js
    const groups = new Map();   // UPDATE 1: stage / slam groups
```

## PATCH #92 — 10. LEVEL LOADER / DISPOSER: stalactites, spires

INSERT AFTER:
```js
      else if (prim.r) _lq.setFromEuler(_le.set(prim.r[0] * DEG, prim.r[1] * DEG, prim.r[2] * DEG));
      else _lq.identity();
      if (prim.t === 'plane') {
```
NEW CODE:
```js
      if (prim.t === 'cone') { this.buildCone(prim, wg, buckets, groups); continue; }   // UPDATE 1: stalactites, spires
```

## PATCH #93 — 10. LEVEL LOADER / DISPOSER: edit: if (surf !== 'CRUMBLING' && prim.roof === undefined && prim.stage === …

FIND:
```js
        col.blocksWarden = prim.block !== undefined ? prim.block : (col.max.y > wg + 2.5 && col.min.y < wg + 9);
        col.wardenPass = !!prim.pass;
        if (surf !== 'CRUMBLING' && prim.roof === undefined) World.add(col);
      }
```
REPLACE WITH:
```js
        col.blocksWarden = prim.block !== undefined ? prim.block : (col.max.y > wg + 2.5 && col.min.y < wg + 9);
        col.wardenPass = !!prim.pass;
        if (surf !== 'CRUMBLING' && prim.roof === undefined && prim.stage === undefined && prim.slam === undefined) World.add(col);
      }
```

## PATCH #94 — 10. LEVEL LOADER / DISPOSER: edit: if (prim.stage !== undefined || prim.slam !== undefined) { this.groupP…

INSERT AFTER:
```js
        continue;
      }
      if (prim.roof !== undefined) {
```
NEW CODE:
```js
      if (prim.stage !== undefined || prim.slam !== undefined) { this.groupPrim(groups, prim, geo, matKey, col); continue; }
```

## PATCH #95 — NEW SECTION — 10. LEVEL LOADER / DISPOSER: cones, and groups of prims that rise, collapse or can be slammed

INSERT AFTER:
```js
      Interact.roofs.push(Interact.add(roof));
    }
  },
```
NEW CODE:
```js
    this.buildGroups(groups);
  },

  // ---------- UPDATE 1: cones, and groups of prims that rise, collapse or can be slammed
  buildCone(prim, wg, buckets, groups) {
    const [rt, rb, h] = prim.s, rm = (rt + rb) / 2, cols = [];
    if (prim.col !== false) for (const k of [-1, 1]) {   // two stacked cylinders approximate the taper
      const r = Math.max(0.03, (k < 0 ? rb + rm : rm + rt) / 2 * 0.92);
      const c = World.makeCyl(_ls.set(0, k * h / 4, 0).applyQuaternion(_lq).add(_lp), _lq, r, h / 4, prim.surf || 'DEFAULT');
      c.blocksWarden = prim.block !== undefined ? prim.block : (c.max.y > wg + 2.5 && c.min.y < wg + 9);
      c.wardenPass = !!prim.pass;
      cols.push(c);
    }
    const geo = new THREE.CylinderGeometry(rt, rb, h, Math.max(rt, rb) < 0.3 ? 7 : 12, 2);
    colorizeGeometry(geo, prim.c === undefined ? 0xffffff : prim.c, 0.12);
    geo.applyMatrix4(_lm.compose(_lp, _lq, _ls.set(1, 1, 1)));
    const mk = prim.m || 'plain';
    worldUV(geo, (MAT_DEFS[mk] || MAT_DEFS.plain).scale);
    if (prim.stage !== undefined || prim.slam !== undefined) { this.groupPrim(groups, prim, geo, mk, cols[0] || null, cols[1]); return; }
    for (const c of cols) World.add(c);
    if (!buckets.has(mk)) buckets.set(mk, []);
    buckets.get(mk).push(geo);
  },
  groupPrim(groups, prim, geo, m, col, col2) {
    const key = prim.slam !== undefined ? 'slam|' + prim.slam : (prim.reveal ? 'reveal|' : 'collapse|') + prim.stage;
    if (!groups.has(key)) groups.set(key, { kind: key.split('|')[0], stage: prim.stage, geos: [], cols: [] });
    const G = groups.get(key);
    G.geos.push({ geo, m });
    if (col) G.cols.push(col);
    if (col2) G.cols.push(col2);
  },
  stage(key) {
    if (!this.stages.has(key)) this.stages.set(key, { reveal: [], collapse: [], done: false });
    return this.stages.get(key);
  },
  buildGroups(groups) {
    for (const [key, G] of groups) {
      const box = new THREE.Box3();
      for (const { geo } of G.geos) { geo.computeBoundingBox(); box.union(geo.boundingBox); }
      const center = box.getCenter(new THREE.Vector3());
      const byMat = new Map();
      for (const { geo, m } of G.geos) { if (!byMat.has(m)) byMat.set(m, []); byMat.get(m).push(geo); }
      const holder = new THREE.Group();
      for (const [m, geos] of byMat) {
        const merged = mergeGeometries(geos); geos.forEach((g) => g.dispose());
        if (G.kind !== 'reveal') merged.translate(-center.x, -center.y, -center.z);
        holder.add(new THREE.Mesh(merged, getMaterial(m)));
      }
      if (G.kind === 'reveal') {   // hidden below until its stage: then it rises into place
        const r = new RevealGroup(G.stage);
        r.holder.add(holder);
        for (const c of G.cols) { addCollider(r, c); c.enabled = false; }
        this.stage(G.stage).reveal.push(r);
        Interact.add(r);
      } else {                     // collapses like a roof (a slammed platform comes back on respawn)
        const roof = new Roof({ id: key, center: center.toArray() });
        roof.addMesh(holder);
        for (const c of G.cols) { World.add(c); roof.colliders.push(c); c.interact = roof; c.blocksWarden = false; }
        if (G.kind === 'slam') { roof.resettable = true; roof.slamPlatform = true; roof.slamPoint = new THREE.Vector3(center.x, box.max.y, center.z); Interact.slams.push(roof); }
        else this.stage(G.stage).collapse.push(roof);
        Interact.add(roof);
      }
    }
  },
  triggerStage(key) {
    const s = this.stages.get(key);
    if (s && !s.done) {
      s.done = true;
      for (const r of s.reveal) r.reveal();
      for (const c of s.collapse) c.collapse();
      if (s.reveal.length) { AudioSys.wetCreak(Player.head, 0.8); AudioSys.thud(Player.head, 0.6); Input.hapticBoth(0.5, 500); }
    }
    for (const l of Interact.lanterns) if (l.dormant && l.stage === key) l.wakeUp();
    Cords.unlockStage(key);
    const D = this.data || {};
    if (D.stageCollapse && D.stageCollapse[key]) for (const k of D.stageCollapse[key]) { const t = this.stages.get(k); if (t) for (const r of t.reveal) r.collapse(); }
    if (D.stageLinks && D.stageLinks[key]) for (const k of D.stageLinks[key]) this.triggerStage(k);
```

## PATCH #96 — 11. UI: helpers

INSERT AFTER:
```js
}

function roundRect(ctx, x, y, w, h, r) {
```
NEW CODE:
```js
// UPDATE 1 helpers
function fmtTime(sec) {
  const t = Math.max(0, sec), m = Math.floor(t / 60), s = t - m * 60;
  return `${m}:${s < 10 ? '0' : ''}${s.toFixed(1)}`;
}
function drawAchievementList(c, W, H) {
  c.clearRect(0, 0, W, H);
  roundRect(c, 4, 4, W - 8, H - 8, 20); c.fillStyle = 'rgba(14,10,8,0.9)'; c.fill();
  ACHIEVEMENTS.forEach((a, i) => {
    const col = i % 2, row = Math.floor(i / 2), x = 26 + col * (W / 2), y = 52 + row * 70;
    const got = Achievements.has(a.id);
    c.textAlign = 'left';
    c.fillStyle = got ? '#ffd27a' : '#6a5a4c'; c.font = 'bold 28px Georgia'; c.fillText((got ? '★ ' : '☆ ') + a.name, x, y);
    c.fillStyle = got ? '#c8b498' : '#7a6a5a'; c.font = 'italic 19px Georgia'; c.fillText(a.hint, x + 32, y + 26);
  });
}
```

## PATCH #97 — 11. UI: long labels shrink to fit

FIND:
```js
      c.fillStyle = !this.enabled ? '#1a1616' : this.hover ? '#6a2a1a' : '#3a1c14'; c.fill();
      c.lineWidth = 4; c.strokeStyle = this.enabled ? '#c08a60' : '#3a3030'; c.stroke();
      c.fillStyle = this.enabled ? '#f2e2c8' : '#5a5050';
      c.font = `bold ${Math.round(H * 0.46)}px Georgia`; c.textAlign = 'center'; c.textBaseline = 'middle';
      c.fillText(this.label, W / 2, H / 2 + 2);
```
REPLACE WITH:
```js
      c.fillStyle = !this.enabled ? '#1a1616' : this.hover ? '#6a2a1a' : '#3a1c14'; c.fill();
      c.lineWidth = 4; c.strokeStyle = this.enabled ? '#c08a60' : '#3a3030'; c.stroke();
      c.fillStyle = this.enabled ? '#f2e2c8' : '#8a7a70';
      let fs = Math.round(H * 0.46);
      c.font = `bold ${fs}px Georgia`; c.textAlign = 'center'; c.textBaseline = 'middle';
      const tw = c.measureText(this.label).width;   // UPDATE 1: long labels shrink to fit
      if (tw > W * 0.9) { fs = Math.max(10, Math.floor(fs * W * 0.9 / tw)); c.font = `bold ${fs}px Georgia`; }
      c.fillText(this.label, W / 2, H / 2 + 2);
```

## PATCH #98 — 11. UI: edit: menu: null, menuPage: 'main', pages: {}, levelMode: 'story',

FIND:
```js
const UI = {
  scene: null, camera: null, buttons: [], globalCool: 0,
  menu: null, menuPage: 'main', pages: {},
  pause: null, pausePage: {},
```
REPLACE WITH:
```js
const UI = {
  scene: null, camera: null, buttons: [], globalCool: 0,
  menu: null, menuPage: 'main', pages: {}, levelMode: 'story',
  pause: null, pausePage: {},
```

## PATCH #99 — 11. UI: two columns of four)

FIND:
```js
    this.menuHead = head;
    const mk = (page) => { const pg = new THREE.Group(); g.add(pg); this.pages[page] = pg; return pg; };
    // main
    const main = mk('main');
    new UIButton(main, 'PLAY', 0.9, 0.2, 0, 0.2, () => Game.play());
    new UIButton(main, 'LEVEL SELECT', 0.9, 0.2, 0, -0.04, () => this.showMenuPage('levels'));
    new UIButton(main, 'SETTINGS', 0.9, 0.2, 0, -0.28, () => this.showMenuPage('settings'));
    this.quitBtn = new UIButton(main, 'QUIT VR', 0.9, 0.2, 0, -0.52, () => Game.quitVR());
    // levels
    const lv = mk('levels');
    this.levelBtns = [];
    for (let i = 0; i < 6; i++) {
      const col = i % 2, row = Math.floor(i / 2);
      this.levelBtns.push(new UIButton(lv, `${i}  ${LEVEL_NAMES[i]}`, 0.85, 0.17, col ? 0.45 : -0.45, 0.22 - row * 0.22, () => Game.selectLevel(i)));
    }
    new UIButton(lv, 'BACK', 0.6, 0.16, 0, -0.52, () => this.showMenuPage('main'));
    // settings
    const st = mk('settings');
    this.setSnap = new UIButton(st, '', 1.1, 0.16, 0, 0.26, () => Game.toggleSetting('snapTurn'));
    this.setVig = new UIButton(st, '', 1.1, 0.16, 0, 0.06, () => Game.toggleSetting('vignette'));
    new UIButton(st, '-', 0.18, 0.16, -0.5, -0.14, () => Game.changeVolume(-0.1));
    this.setVol = new UIButton(st, '', 0.7, 0.16, 0, -0.14, () => {});
    new UIButton(st, '+', 0.18, 0.16, 0.5, -0.14, () => Game.changeVolume(0.1));
    this.setScare = new UIButton(st, '', 1.1, 0.16, 0, -0.34, () => Game.toggleSetting('reducedScares'));
    new UIButton(st, 'BACK', 0.6, 0.14, 0, -0.55, () => this.showMenuPage('main'));
    this.scene.add(g);
```
REPLACE WITH:
```js
    this.menuHead = head;
    const mk = (page) => { const pg = new THREE.Group(); g.add(pg); this.pages[page] = pg; return pg; };
    const back = (pg, to = 'main') => new UIButton(pg, 'BACK', 0.6, 0.13, 0, -0.6, () => this.showMenuPage(to));
    // main (UPDATE 1: two columns of four)
    const main = mk('main');
    const mainBtns = [['PLAY', () => Game.play()], ['MODES', () => this.showMenuPage('modes')],
      ['LEVEL SELECT', () => { this.levelMode = 'story'; this.showMenuPage('levels'); }], ['SHELF', () => this.showMenuPage('shelf')],
      ['NOTES', () => this.showMenuPage('notes')], ['ACHIEVEMENTS', () => this.showMenuPage('achievements')],
      ['SETTINGS', () => this.showMenuPage('settings')], ['QUIT VR', () => Game.quitVR()]];
    mainBtns.forEach(([label, fn], i) => {
      const b = new UIButton(main, label, 0.85, 0.17, i % 2 ? 0.45 : -0.45, 0.24 - Math.floor(i / 2) * 0.24, fn);
      if (label === 'QUIT VR') this.quitBtn = b;
    });
    // modes
    const md = mk('modes');
    this.modeBtns = {
      story: new UIButton(md, 'STORY', 1.3, 0.15, 0, 0.26, () => { this.levelMode = 'story'; this.showMenuPage('levels'); }),
      nightmare: new UIButton(md, '', 1.3, 0.15, 0, 0.08, () => { this.levelMode = 'nightmare'; this.showMenuPage('levels'); }),
      endless: new UIButton(md, '', 1.3, 0.15, 0, -0.1, () => Game.startEndless(1)),
      timetrial: new UIButton(md, '', 1.3, 0.15, 0, -0.28, () => { this.levelMode = 'timetrial'; this.showMenuPage('levels'); }),
    };
    back(md);
    // levels: 3 x 3, shared by Story, Nightmare and Time Trial
    const lv = mk('levels');
    this.levelBtns = [];
    for (let i = 0; i < 9; i++) {
      this.levelBtns.push(new UIButton(lv, `${i}  ${LEVEL_NAMES[i]}`, 0.58, 0.16, (i % 3 - 1) * 0.61, 0.24 - Math.floor(i / 3) * 0.21, () => Game.selectLevel(i, this.levelMode)));
    }
    back(lv);
    // shelf: cosmetics unlocked by toys
    const sh = mk('shelf');
    this.shelfBtns = COSMETICS.map((c, i) => new UIButton(sh, c.name, 0.58, 0.16, (i % 3 - 1) * 0.61, 0.24 - Math.floor(i / 3) * 0.21, () => Cosmetics.choose(c)));
    back(sh);
    // notes: read what you have found
    const nt = mk('notes');
    this.noteBtns = [];
    for (let i = 0; i < 18; i++) this.noteBtns.push(new UIButton(nt, '', 0.58, 0.1, (i % 3 - 1) * 0.61, 0.28 - Math.floor(i / 3) * 0.135, () => Notes.show(i, 0.9)));
    back(nt);
    // achievements
    const ac = mk('achievements');
    this.achPanel = new CanvasPanel(1.8, 0.95, 1024, 540);
    this.achPanel.mesh.position.set(0, -0.03, 0.002); ac.add(this.achPanel.mesh);
    back(ac);
    // settings (UPDATE 1: two columns)
    const st = mk('settings');
    const T = (key, col, row) => new UIButton(st, '', 0.85, 0.15, col ? 0.45 : -0.45, 0.26 - row * 0.19, () => Game.toggleSetting(key));
    this.setSnap = T('snapTurn', 0, 0); this.setVig = T('vignette', 0, 1); this.setScare = T('reducedScares', 0, 2);
    this.setArach = T('arachnophobia', 1, 0); this.setSubs = T('subtitles', 1, 2);
    this.setGrip = new UIButton(st, '', 0.85, 0.15, 0.45, 0.07, () => Game.toggleGripMode());
    new UIButton(st, '-', 0.18, 0.15, -0.5, -0.38, () => Game.changeVolume(-0.1));
    this.setVol = new UIButton(st, '', 0.7, 0.15, 0, -0.38, () => {});
    new UIButton(st, '+', 0.18, 0.15, 0.5, -0.38, () => Game.changeVolume(0.1));
    back(st);
    this.scene.add(g);
```

## PATCH #100 — 11. UI: edit: const lvTitle = { story: ['LEVEL SELECT', 'finished levels unlock the …

FIND:
```js
    this.menuPage = p;
    for (const k in this.pages) this.pages[k].visible = k === p;
    const titles = { main: ['HOLLOWMAW', 'touch a button with your hand'], levels: ['LEVEL SELECT', 'finished levels unlock the next'], settings: ['SETTINGS', 'comfort & sound'] };
    this.menuHead.draw((c, W, H) => {
```
REPLACE WITH:
```js
    this.menuPage = p;
    for (const k in this.pages) this.pages[k].visible = k === p;
    const lvTitle = { story: ['LEVEL SELECT', 'finished levels unlock the next'], nightmare: ['NIGHTMARE', 'the Hollow Warden · half the lanterns · no batteries'], timetrial: ['TIME TRIAL', 'no Warden · beat your ghost'] }[this.levelMode];
    const titles = { main: ['HOLLOWMAW', 'touch a button with your hand'], levels: lvTitle, settings: ['SETTINGS', 'comfort, sound & grip'],
      modes: ['MODES', 'story · nightmare · endless · time trial'], shelf: ['THE SHELF', 'carved toys unlock things to wear'],
      notes: ['NOTES', 'what the children wrote'], achievements: ['ACHIEVEMENTS', `${Achievements.count()} of ${ACHIEVEMENTS.length}`] };
    if (p === 'achievements') this.achPanel.draw((c, W, H) => drawAchievementList(c, W, H));
    this.menuHead.draw((c, W, H) => {
```

## PATCH #101 — 11. UI: edit: const S = Game.progress.settings, P = Game.progress;

FIND:
```js
  },
  refreshSettings() {
    const S = Game.progress.settings;
    const onoff = (b) => (b ? 'ON' : 'OFF');
```
REPLACE WITH:
```js
  },
  refreshSettings() {
    const S = Game.progress.settings, P = Game.progress;
    const onoff = (b) => (b ? 'ON' : 'OFF');
```

## PATCH #102 — 11. UI: edit: this.setArach.setLabel(`ARACHNOPHOBIA MODE: ${onoff(S.arachnophobia)}`…

INSERT AFTER:
```js
    this.setVol.setLabel(`VOLUME ${Math.round(S.volume * 100)}%`);
    this.setScare.setLabel(`REDUCED SCARES: ${onoff(S.reducedScares)}`);
    if (this.pSnap) {
```
NEW CODE:
```js
    this.setArach.setLabel(`ARACHNOPHOBIA MODE: ${onoff(S.arachnophobia)}`);
    this.setSubs.setLabel(`SUBTITLES: ${onoff(S.subtitles)}`);
    this.setGrip.setLabel(`GRAB: ${S.gripMode === 'toggle' ? 'TOGGLE' : 'HOLD'}`);
```

## PATCH #103 — 11. UI: levels per mode, with hints on locked buttons

FIND:
```js
      this.pVol.setLabel(`VOLUME ${Math.round(S.volume * 100)}%`);
      this.pScare.setLabel(`REDUCED SCARES: ${onoff(S.reducedScares)}`);
    }
    if (this.levelBtns) this.levelBtns.forEach((b, i) => { b.setEnabled(i <= Game.progress.unlocked); b.setLabel(i <= Game.progress.unlocked ? `${i}  ${LEVEL_NAMES[i]}${Game.progress.toys[i] ? ' *' : ''}` : `${i}  LOCKED`); });
    if (this.quitBtn) this.quitBtn.setEnabled(Input.xr);
```
REPLACE WITH:
```js
      this.pVol.setLabel(`VOLUME ${Math.round(S.volume * 100)}%`);
      this.pScare.setLabel(`REDUCED SCARES: ${onoff(S.reducedScares)}`);
      this.pArach.setLabel(`ARACHNOPHOBIA: ${onoff(S.arachnophobia)}`);
      this.pSubs.setLabel(`SUBTITLES: ${onoff(S.subtitles)}`);
      this.pGrip.setLabel(`GRAB: ${S.gripMode === 'toggle' ? 'TOGGLE' : 'HOLD'}`);
    }
    // UPDATE 1: levels per mode, with hints on locked buttons
    const mode = this.levelMode;
    if (this.levelBtns) this.levelBtns.forEach((b, i) => {
      const ok = Game.levelAvailable(i, mode);
      b.setEnabled(ok);
      if (!ok) b.setLabel(`${i}  ${Game.lockHint(i, mode)}`);
      else if (mode === 'timetrial') b.setLabel(`${i}  ${LEVEL_NAMES[i]}  ${P.timeTrial.best[i] ? fmtTime(P.timeTrial.best[i]) : '--:--'}`);
      else b.setLabel(`${i}  ${LEVEL_NAMES[i]}${P.toys[i] ? ' *' : ''}`);
    });
    if (this.modeBtns) {
      const M = this.modeBtns, anyDone = P.unlocked > 0 || P.endings.true;
      M.nightmare.setEnabled(P.endings.true); M.nightmare.setLabel(P.endings.true ? 'NIGHTMARE' : 'NIGHTMARE  (reach the true ending)');
      M.endless.setEnabled(P.endings.first); M.endless.setLabel(P.endings.first ? `ENDLESS DESCENT   BEST: ${P.endless.best} FLOORS` : 'ENDLESS DESCENT  (finish The Escape)');
      M.timetrial.setEnabled(anyDone); M.timetrial.setLabel(anyDone ? 'TIME TRIAL' : 'TIME TRIAL  (finish any level)');
    }
    if (this.shelfBtns) this.shelfBtns.forEach((b, i) => {
      const c = COSMETICS[i];
      b.setLabel(Cosmetics.unlocked(c) ? (Cosmetics.equipped(c) ? '> ' + c.name + ' <' : c.name) : `${c.toys} TOYS TO UNLOCK`);
    });
    if (this.noteBtns) this.noteBtns.forEach((b, i) => { b.setEnabled(!!P.notes[i]); b.setLabel(P.notes[i] ? `${LEVEL_NAMES[i >> 1].replace('THE ', '')} · ${(i & 1) + 1}` : `???  (level ${i >> 1})`); });
    if (this.quitBtn) this.quitBtn.setEnabled(Input.xr);
```

## PATCH #104 — 11. UI: this.pSubs = B('', -0.13, () => Game.toggleSetting('subtitles'));

FIND:
```js
  buildPause() {
    const g = new THREE.Group(); g.visible = false; this.pause = g;
    const bg = new CanvasPanel(0.64, 0.86, 512, 688);
    bg.draw((c, W, H) => { roundRect(c, 4, 4, W - 8, H - 8, 30); c.fillStyle = 'rgba(12,8,6,0.92)'; c.fill(); c.strokeStyle = '#7a5a40'; c.lineWidth = 6; c.stroke();
      c.fillStyle = '#e8d8c0'; c.font = 'bold 56px Georgia'; c.textAlign = 'center'; c.fillText('PAUSED', W / 2, 72); });
    bg.mesh.position.z = -0.02; g.add(bg.mesh);
    const B = (label, y, fn, w = 0.5) => new UIButton(g, label, w, 0.075, 0, y, fn);
    B('RESUME', 0.27, () => Game.resume());
    B('BACK TO LANTERN', 0.18, () => Game.restartCheckpoint());
    this.pSnap = B('', 0.07, () => Game.toggleSetting('snapTurn'));
    this.pVig = B('', -0.02, () => Game.toggleSetting('vignette'));
    this.pScare = B('', -0.11, () => Game.toggleSetting('reducedScares'));
    new UIButton(g, '-', 0.08, 0.075, -0.21, -0.2, () => Game.changeVolume(-0.1));
    this.pVol = new UIButton(g, '', 0.3, 0.075, 0, -0.2, () => {});
    new UIButton(g, '+', 0.08, 0.075, 0.21, -0.2, () => Game.changeVolume(0.1));
    B('MAIN MENU', -0.32, () => Game.toMainMenu());
    this.scene.add(g);
```
REPLACE WITH:
```js
  buildPause() {
    const g = new THREE.Group(); g.visible = false; this.pause = g;
    const bg = new CanvasPanel(0.64, 1.04, 512, 832);
    bg.draw((c, W, H) => { roundRect(c, 4, 4, W - 8, H - 8, 30); c.fillStyle = 'rgba(12,8,6,0.92)'; c.fill(); c.strokeStyle = '#7a5a40'; c.lineWidth = 6; c.stroke();
      c.fillStyle = '#e8d8c0'; c.font = 'bold 56px Georgia'; c.textAlign = 'center'; c.fillText('PAUSED', W / 2, 62); });
    bg.mesh.position.z = -0.02; g.add(bg.mesh);
    const B = (label, y, fn, w = 0.5) => new UIButton(g, label, w, 0.068, 0, y, fn);
    B('RESUME', 0.36, () => Game.resume());
    B('BACK TO LANTERN', 0.28, () => Game.restartCheckpoint());
    this.pSnap = B('', 0.19, () => Game.toggleSetting('snapTurn'));
    this.pVig = B('', 0.11, () => Game.toggleSetting('vignette'));
    this.pScare = B('', 0.03, () => Game.toggleSetting('reducedScares'));
    this.pArach = B('', -0.05, () => Game.toggleSetting('arachnophobia'));   // UPDATE 1
    this.pSubs = B('', -0.13, () => Game.toggleSetting('subtitles'));
    this.pGrip = B('', -0.21, () => Game.toggleGripMode());
    new UIButton(g, '-', 0.08, 0.068, -0.21, -0.3, () => Game.changeVolume(-0.1));
    this.pVol = new UIButton(g, '', 0.3, 0.068, 0, -0.3, () => {});
    new UIButton(g, '+', 0.08, 0.068, 0.21, -0.3, () => Game.changeVolume(0.1));
    B('MAIN MENU', -0.42, () => Game.toMainMenu());
    this.scene.add(g);
```

## PATCH #105 — 11. UI: kind = 'first' (The Escape), 'true' (The Heart), 'endless', 'timetrial'

FIND:
```js
    this.scene.add(g);
  },
  showEnd(stats) {
    const t = Math.floor(stats.time), mm = Math.floor(t / 60), ss = String(t % 60).padStart(2, '0');
    const toys = Game.progress.toys.filter(Boolean).length;
    this.endText.draw((c, W, H) => {
      roundRect(c, 6, 6, W - 12, H - 12, 40); c.fillStyle = 'rgba(8,4,4,0.9)'; c.fill(); c.strokeStyle = '#8a3020'; c.lineWidth = 8; c.stroke();
      c.textAlign = 'center'; c.fillStyle = '#f0e0c8'; c.font = 'bold 110px Georgia'; c.fillText('YOU ESCAPED', W / 2, 150);
      c.font = '48px Georgia'; c.fillStyle = '#d0b898';
      c.fillText(`Time  ${mm}:${ss}`, W / 2, 280);
      c.fillText(`Deaths  ${stats.deaths}`, W / 2, 350);
      c.fillText(`Carved toys found  ${toys} / 6`, W / 2, 420);
      c.font = 'italic 34px Georgia'; c.fillStyle = '#8a7a68';
      c.fillText('Behind you, the gate holds. For now.', W / 2, 500);
    });
```
REPLACE WITH:
```js
    this.scene.add(g);
  },
  // UPDATE 1: kind = 'first' (The Escape), 'true' (The Heart), 'endless', 'timetrial'
  showEnd(stats, kind = 'first', extra = {}) {
    const P = Game.progress;
    const toys = P.toys.filter(Boolean).length, notes = P.notes.filter(Boolean).length;
    const head = { first: 'YOU ESCAPED', true: 'TRUE ENDING', endless: 'THE DARK TOOK YOU', timetrial: extra.record ? 'NEW RECORD' : 'TIME TRIAL' }[kind];
    const rows = kind === 'endless' ? [`Floors survived  ${extra.floors}`, `Best  ${P.endless.best}`, `Time  ${fmtTime(stats.time)}`]
      : kind === 'timetrial' ? [LEVEL_NAMES[Game.levelIndex], `Time  ${fmtTime(stats.time)}`, `Best  ${fmtTime(P.timeTrial.best[Game.levelIndex])}`]
      : [`Time  ${fmtTime(stats.time)}`, `Deaths  ${stats.deaths}`, `Carved toys  ${toys} / 9     Notes  ${notes} / 18`];
    const foot = { first: 'Behind the gate, the ground is cracking open. A hole has opened in the Playground.', true: 'He can sleep now. Thank you.',
      endless: 'It goes deeper. It always goes deeper.', timetrial: 'Your ghost will race you next time.' }[kind];
    this.endText.draw((c, W, H) => {
      roundRect(c, 6, 6, W - 12, H - 12, 40); c.fillStyle = kind === 'true' ? 'rgba(20,14,8,0.9)' : 'rgba(8,4,4,0.9)'; c.fill();
      c.strokeStyle = kind === 'true' ? '#d0a040' : '#8a3020'; c.lineWidth = 8; c.stroke();
      c.textAlign = 'center'; c.fillStyle = '#f0e0c8'; c.font = 'bold 100px Georgia'; c.fillText(head, W / 2, 150);
      c.font = '46px Georgia'; c.fillStyle = '#d0b898';
      rows.forEach((r, i) => c.fillText(r, W / 2, 280 + i * 70));
      if (kind === 'true') { c.font = '34px Georgia'; c.fillStyle = '#c8a870'; c.fillText(`Achievements  ${Achievements.count()} / ${ACHIEVEMENTS.length}   ·   Nightmare mode unlocked`, W / 2, 500); }
      c.font = 'italic 32px Georgia'; c.fillStyle = '#8a7a68';
      drawTextBlock(c, foot, W / 2, kind === 'true' ? 560 : 520, W - 120, 38);
    });
```

## PATCH #106 — 11. UI: objectives

FIND:
```js
    else if (O.type === 'lantern') prog = O.done ? 'LANTERN LIT - FIND THE DRAIN' : 'TREEHOUSE LANTERN: UNLIT';
    else if (O.type === 'escape') prog = 'RUN';
    if (O.done && O.type !== 'lantern' && O.type !== 'escape') prog = 'DONE - FIND THE WAY OUT';
    const bat = Math.round(Flashlight.battery * 100);
    const toys = Game.progress.toys.filter(Boolean).length;
    const key = `${L.name}|${prog}|${bat}|${toys}|${Flashlight.on}|${Game.state}`;
    if (key === this.wristKey) return;
```
REPLACE WITH:
```js
    else if (O.type === 'lantern') prog = O.done ? 'LANTERN LIT - FIND THE DRAIN' : 'TREEHOUSE LANTERN: UNLIT';
    else if (O.type === 'escape') prog = 'RUN';
    // UPDATE 1 objectives
    else if (O.type === 'stones') prog = `STONES  ${O.have} / ${O.need}`;
    else if (O.type === 'chapelbell') prog = O.done ? 'CLIMB OUT THROUGH THE ROOF' : 'RING THE BELL';
    else if (O.type === 'cord') prog = O.done ? 'CLIMB TO THE LIGHT' : `CORDS CUT  ${O.have} / ${O.need}`;
    else if (O.type === 'descend') prog = `FLOOR ${Game.endless.floor} - FIND THE PIT`;
    if (O.done && O.type !== 'lantern' && O.type !== 'escape' && O.type !== 'chapelbell' && O.type !== 'cord') prog = 'DONE - FIND THE WAY OUT';
    const bat = Math.round(Flashlight.battery * 100);
    const toys = Game.progress.toys.filter(Boolean).length;
    const tag = Game.modeTag();
    const status = Game.wristStatus();
    const key = `${L.name}|${prog}|${bat}|${toys}|${Flashlight.on}|${Game.state}|${tag}|${status}`;
    if (key === this.wristKey) return;
```

## PATCH #107 — 11. UI: edit: if (tag) { c.textAlign = 'right'; c.fillStyle = Game.mode === 'nightma…

FIND:
```js
      roundRect(c, 4, 4, W - 8, H - 8, 22); c.fillStyle = 'rgba(14,10,8,0.9)'; c.fill(); c.strokeStyle = '#6a4a30'; c.lineWidth = 5; c.stroke();
      c.fillStyle = '#f0c890'; c.font = 'bold 30px Georgia'; c.textAlign = 'left'; c.fillText(L.name, 18, 42);
      c.fillStyle = '#d8ccb8'; c.font = '22px Georgia'; drawTextBlock(c, L.objectiveText, 18, 76, W - 36, 26, 'left');
      c.fillStyle = '#ffd890'; c.font = 'bold 24px Georgia'; c.fillText(prog, 18, 176);
      c.fillStyle = '#a89880'; c.font = '20px Georgia'; c.fillText(`TOYS ${toys}/6`, 18, 206);
      // battery
```
REPLACE WITH:
```js
      roundRect(c, 4, 4, W - 8, H - 8, 22); c.fillStyle = 'rgba(14,10,8,0.9)'; c.fill(); c.strokeStyle = '#6a4a30'; c.lineWidth = 5; c.stroke();
      c.fillStyle = '#f0c890'; c.font = 'bold 30px Georgia'; c.textAlign = 'left'; c.fillText(L.name, 18, 42);
      if (tag) { c.textAlign = 'right'; c.fillStyle = Game.mode === 'nightmare' ? '#ff6050' : '#90c8ff'; c.font = 'bold 20px Georgia'; c.fillText(tag, W - 16, 40); c.textAlign = 'left'; }
      if (status) { c.fillStyle = status.startsWith('CRAWLER') || status.startsWith('AIR') ? '#ff7050' : '#a8d8c0'; c.font = 'bold 20px Georgia'; c.fillText(status, 18, 146); }
      c.fillStyle = '#d8ccb8'; c.font = '20px Georgia'; drawTextBlock(c, L.objectiveText, 18, 72, W - 36, 22, 'left');
      c.fillStyle = '#ffd890'; c.font = 'bold 24px Georgia'; c.fillText(prog, 18, 176);
      c.fillStyle = '#a89880'; c.font = '20px Georgia'; c.fillText(`TOYS ${toys}/9`, 18, 206);
      // battery
```

## PATCH #108 — 12. GAME STATE MANAGER: save version 2. A v1 save is read once and migrated (unlocked levels, toys and settings ke

FIND:
```js
   12. GAME STATE MANAGER — menu, playing, caught, level complete, end
   ===================================================================== */
const STORE_KEY = 'hollowmaw_progress_v1';
const Store = {
  load() { try { const s = localStorage.getItem(STORE_KEY); return s ? JSON.parse(s) : null; } catch (e) { return null; } },
  save(o) { try { localStorage.setItem(STORE_KEY, JSON.stringify(o)); } catch (e) { /* storage unavailable */ } },
```
REPLACE WITH:
```js
   12. GAME STATE MANAGER — menu, playing, caught, level complete, end
   ===================================================================== */
// UPDATE 1: save version 2. A v1 save is read once and migrated (unlocked levels, toys and settings kept).
const STORE_KEY = U1.SAVE_KEY;
const Store = {
  load() {
    try {
      const s = localStorage.getItem(STORE_KEY);
      if (s) return JSON.parse(s);
      const old = localStorage.getItem(U1.OLD_SAVE_KEY);
      return old ? this.migrate(JSON.parse(old)) : null;
    } catch (e) { return null; }
  },
  migrate(v1) {
    return { version: U1.SAVE_VERSION, migratedFrom: 1, unlocked: clamp(v1.unlocked | 0, 0, 5), toys: Array.isArray(v1.toys) ? v1.toys.slice(0, 6) : [], settings: v1.settings || {} };
  },
  save(o) { try { localStorage.setItem(STORE_KEY, JSON.stringify(o)); } catch (e) { /* storage unavailable */ } },
```

## PATCH #109 — 12. GAME STATE MANAGER: modes and per-run state

FIND:
```js
  inventory: { fuses: 0 },
  stats: { time: 0, deaths: 0, running: false },
  progress: { unlocked: 0, toys: [false, false, false, false, false, false], settings: { snapTurn: true, vignette: false, volume: 0.8, reducedScares: false } },
  playerLight: 0.5, lightT: 0, fear: 0,
```
REPLACE WITH:
```js
  inventory: { fuses: 0 },
  stats: { time: 0, deaths: 0, running: false },
  progress: {
    version: U1.SAVE_VERSION, unlocked: 0, toys: new Array(9).fill(false),
    settings: { snapTurn: true, vignette: false, volume: 0.8, reducedScares: false, arachnophobia: false, gripMode: 'hold', subtitles: false },
    endings: { first: false, true: false }, notes: new Array(18).fill(false), achievements: {},
    cosmetics: { fur: 'fur_default', bracelet: false, lantern: false, crown: false },
    stats: { crawlersRemoved: 0, canopyBells: false, chapelBell: false },
    endless: { best: 0 }, timeTrial: { best: new Array(9).fill(0) }, lastCatch: {},
  },
  // UPDATE 1: modes and per-run state
  mode: 'story', endless: { floor: 1, seed: 1 }, huntedThisLevel: false, checkpointWater: {}, outroT: 0, outroFrom: null,
  playerLight: 0.5, lightT: 0, fear: 0,
```

## PATCH #110 — 12. GAME STATE MANAGER: testing on a headset (no debug keys there)

FIND:
```js
    const saved = Store.load();
    if (saved) {
      if (typeof saved.unlocked === 'number') this.progress.unlocked = clamp(saved.unlocked, 0, 5);
      if (Array.isArray(saved.toys)) saved.toys.forEach((t, i) => { if (i < 6) this.progress.toys[i] = !!t; });
      if (saved.settings) Object.assign(this.progress.settings, saved.settings);
    }
    AudioSys.volume = this.progress.settings.volume;
```
REPLACE WITH:
```js
    const saved = Store.load();
    if (saved) {
      this.mergeSave(saved);
      if (saved.migratedFrom) this.saveProgress();   // write the v2 save right away
    }
    if (/[?&]unlockall\b/.test(window.location.search)) setTimeout(() => this.unlockAll(), 0);   // UPDATE 1: testing on a headset (no debug keys there)
    AudioSys.volume = this.progress.settings.volume;
```

## PATCH #111 — 12. GAME STATE MANAGER: Copy a saved object into the defaults field by field (unknown or malformed field

FIND:
```js
    scene.add(this.faceLight);
  },
  saveProgress() { Store.save({ unlocked: this.progress.unlocked, toys: this.progress.toys, settings: this.progress.settings }); },

  physicsActive() { return this.state === 'PLAYING' || this.state === 'MENU' || this.state === 'ENDING'; },

```
REPLACE WITH:
```js
    scene.add(this.faceLight);
  },
  saveProgress() { Store.save(this.progress); },
  // Copy a saved object into the defaults field by field (unknown or malformed fields are ignored)
  mergeSave(s) {
    const P = this.progress;
    if (typeof s.unlocked === 'number') P.unlocked = clamp(s.unlocked, 0, 8);
    if (Array.isArray(s.toys)) s.toys.forEach((t, i) => { if (i < 9) P.toys[i] = !!t; });
    if (s.settings) for (const k in P.settings) if (s.settings[k] !== undefined && typeof s.settings[k] === typeof P.settings[k]) P.settings[k] = s.settings[k];
    if (P.settings.gripMode !== 'toggle') P.settings.gripMode = 'hold';
    if (s.endings) { P.endings.first = !!s.endings.first; P.endings.true = !!s.endings.true; }
    if (Array.isArray(s.notes)) s.notes.forEach((t, i) => { if (i < 18) P.notes[i] = !!t; });
    if (s.achievements) for (const a of ACHIEVEMENTS) if (s.achievements[a.id]) P.achievements[a.id] = true;
    if (s.cosmetics) {
      if (COSMETICS.some((c) => c.id === s.cosmetics.fur)) P.cosmetics.fur = s.cosmetics.fur;
      for (const k of ['bracelet', 'lantern', 'crown']) P.cosmetics[k] = !!s.cosmetics[k];
    }
    if (s.stats) { P.stats.crawlersRemoved = s.stats.crawlersRemoved | 0; P.stats.canopyBells = !!s.stats.canopyBells; P.stats.chapelBell = !!s.stats.chapelBell; }
    if (s.endless) P.endless.best = s.endless.best | 0;
    if (s.timeTrial && Array.isArray(s.timeTrial.best)) s.timeTrial.best.forEach((t, i) => { if (i < 9) P.timeTrial.best[i] = +t || 0; });
    if (s.lastCatch) for (const k in s.lastCatch) if (Array.isArray(s.lastCatch[k]) && s.lastCatch[k].length === 3) P.lastCatch[k] = s.lastCatch[k].map(Number);
    if (P.endings.first) P.unlocked = Math.max(P.unlocked, 6);
  },

  physicsActive() { return this.state === 'PLAYING' || this.state === 'MENU' || this.state === 'ENDING' || this.state === 'OUTRO'; },

```

## PATCH #112 — 12. GAME STATE MANAGER: this.huntedThisLevel = false;

INSERT AFTER:
```js
    this.checkpointLantern = null;
    this.checkpointYaw = this.levelData.spawn.yaw || 0;
    Player.placeHeadAt(this.checkpoint, this.checkpointYaw);
```
NEW CODE:
```js
    Water.snapshot(this.checkpointWater);   // UPDATE 1
    this.huntedThisLevel = false;
```

## PATCH #113 — 12. GAME STATE MANAGER: Time Trial recorder / best-run ghost

INSERT AFTER:
```js
    UI.wristKey = '';
    this.fear = 0;
  },
```
NEW CODE:
```js
    Ghost.start();   // UPDATE 1: Time Trial recorder / best-run ghost
```

## PATCH #114 — 12. GAME STATE MANAGER: the level select serves Story, Nightmare and Time Trial

FIND:
```js
  },
  play() {
    this.stats = { time: 0, deaths: 0, running: true };
    this.transition(() => this.loadLevel(0, 'PLAYING'));
  },
  selectLevel(i) {
    if (i > this.progress.unlocked) return;
    this.stats = { time: 0, deaths: 0, running: true };
    this.transition(() => this.loadLevel(i, 'PLAYING'));
  },
  toMainMenu() {
```
REPLACE WITH:
```js
  },
  play() {
    this.mode = 'story';
    this.stats = { time: 0, deaths: 0, running: true };
    this.transition(() => this.loadLevel(0, 'PLAYING'));
  },
  // UPDATE 1: the level select serves Story, Nightmare and Time Trial
  selectLevel(i, mode = 'story') {
    if (!this.levelAvailable(i, mode)) return;
    this.mode = mode;
    this.stats = { time: 0, deaths: 0, running: true };
    this.transition(() => this.loadLevel(i, 'PLAYING'));
  },
  levelFinished(i) { return i < this.progress.unlocked || (i === 8 && this.progress.endings.true); },
  levelAvailable(i, mode) {
    if (mode === 'timetrial') return this.levelFinished(i);
    if (mode === 'nightmare' && !this.progress.endings.true) return false;
    return i <= this.progress.unlocked;
  },
  lockHint(i, mode) {
    if (mode === 'timetrial') return 'FINISH IT FIRST';
    if (i >= 6 && !this.progress.endings.first) return 'FINISH THE ESCAPE';
    return 'FINISH ' + LEVEL_NAMES[i - 1].replace('THE ', '');
  },
  modeTag() {
    if (this.mode === 'nightmare') return 'NIGHTMARE';
    if (this.mode === 'endless') return `FLOOR ${this.endless.floor}`;
    if (this.mode === 'timetrial') return fmtTime(this.stats.time);
    return '';
  },
  wristStatus() {
    for (const h of Player.hands) if (h.cling) return 'CRAWLER! SHAKE IT OFF';
    if (Water.active && Water.headUnder) return `AIR ${Math.max(0, Math.ceil(U1.DROWN_TIME - Water.drownT))}s`;
    if (Hiding.current) return 'HIDDEN - HOLD STILL';
    if (Warden.mode === 'sleep') return 'IT SLEEPS  ' + '|'.repeat(Math.round(Warden.wake * 10)).padEnd(10, '.');
    for (const h of Player.hands) if (h.holding) return h.holding.lit ? `FLARE ${Math.ceil(h.holding.litT)}s` : 'HOLDING ' + h.holding.type.toUpperCase();
    if (Water.active && Water.target < Water.max) return `WATER RISES IN ${Math.max(0, Math.ceil(Water.timer))}s`;
    return '';
  },
  startEndless(floor = 1) {
    if (this.state === 'TRANSITION') return;
    this.mode = 'endless';
    this.endless.floor = floor;
    if (floor === 1) this.endless.seed = 1 + Math.floor(Math.random() * 99999);
    this.stats = { time: 0, deaths: 0, running: true };
    UI.showPause(false); UI.end.visible = false;
    this.transition(() => { this.restoreWorld(); this.loadLevel(9, 'PLAYING'); });
  },
  endlessNext() {
    const survived = this.endless.floor;
    this.progress.endless.best = Math.max(this.progress.endless.best, survived);
    this.saveProgress();
    this.endless.floor++;
    if (this.endless.floor >= 10) Achievements.award('deepdiver');
    AudioSys.whoosh(Player.head, 0.6);
    this.transition(() => this.loadLevel(9, 'PLAYING'), 1 / 1.2);
  },
  endlessOver() {
    const survived = this.endless.floor - 1;
    this.progress.endless.best = Math.max(this.progress.endless.best, survived);
    this.saveProgress();
    this.toEndScreen('endless', { floors: survived });
  },
  onPit(exit) {
    if (this.state !== 'PLAYING') return;
    if (this.mode === 'endless') { this.endlessNext(); return; }
    this.enterDeeperDark();
  },
  enterDeeperDark() {   // the hole in the Playground: Story continues at The Nest
    this.mode = 'story';
    AudioSys.whoosh(Player.head, 0.8);
    this.transition(() => this.loadLevel(6, 'PLAYING'), 1 / 1.5);
  },
  finishTimeTrial() {
    const i = this.levelIndex, t = this.stats.time, B = this.progress.timeTrial.best;
    const record = !B[i] || t < B[i];
    if (record) { B[i] = +t.toFixed(2); this.saveProgress(); Ghost.save(); Achievements.award('quickhands'); }
    this.toEndScreen('timetrial', { record });
  },
  toEndScreen(kind, extra) {
    this.stats.running = false;
    this.state = 'TRANSITION';
    this.fadeTarget = 1; this.fadeSpeed = 1 / 1.5;
    this.fadeCb = () => {
      this.restoreWorld();
      Level.hideMeshes(); Warden.root.visible = false; Warden.active = false;
      for (const h of Player.hands) { h.cling = null; h.holding = null; h.cord = null; }
      Crawlers.clear(); Grab.clear();
      this.scene.fog.color.setHex(0x000000); this.scene.background.setHex(0x000000);
      this.state = 'END';
      UI.showEnd(this.stats, kind, extra);
      this.fadeTarget = 0;
    };
  },
  unlockAll() {
    const P = this.progress;
    P.unlocked = 8; P.endings.first = true; P.endings.true = true;
    P.toys.fill(true); P.notes.fill(true);
    this.saveProgress(); UI.refreshSettings(); Hub.refreshShelf();
    this.toast('EVERYTHING UNLOCKED');
  },
  toggleGripMode() { const S = this.progress.settings; S.gripMode = S.gripMode === 'toggle' ? 'hold' : 'toggle'; this.saveProgress(); UI.refreshSettings(); },
  toMainMenu() {
```

## PATCH #115 — 12. GAME STATE MANAGER: if (this.levelData.trueEnding) { this.onTrueEnding(); return; }

FIND:
```js
  levelComplete() {
    if (this.state !== 'PLAYING') return;
    const next = this.levelIndex + 1;
    this.progress.unlocked = Math.max(this.progress.unlocked, Math.min(5, next));
    this.saveProgress();
    AudioSys.whoosh(Player.head, 0.6);
    this.transition(() => this.loadLevel(Math.min(5, next), 'PLAYING'), 1 / 1.2);
  },
```
REPLACE WITH:
```js
  levelComplete() {
    if (this.state !== 'PLAYING') return;
    this.onLevelFinished();
    if (this.mode === 'timetrial') { this.finishTimeTrial(); return; }   // UPDATE 1
    if (this.levelData.trueEnding) { this.onTrueEnding(); return; }
    if (this.mode === 'endless') return;
    const next = this.levelIndex + 1;
    this.progress.unlocked = Math.max(this.progress.unlocked, Math.min(8, next));
    this.saveProgress();
    AudioSys.whoosh(Player.head, 0.6);
    this.transition(() => this.loadLevel(Math.min(8, next), 'PLAYING'), 1 / 1.2);
  },
  // UPDATE 1: achievements that are judged when a level is finished
  onLevelFinished() {
    const W = this.levelData.warden || {};
    if (this.mode !== 'timetrial' && !this.huntedThisLevel && (W.mode === 'normal' || W.mode === 'sleep') && W.canSee !== false) Achievements.award('neverseen');
    if (this.levelIndex === 6 && !Warden.everWoke && this.mode !== 'timetrial') Achievements.award('deepsleeper');
    if (this.mode === 'nightmare') Achievements.award('nightmare');
  },
```

## PATCH #116 — 12. GAME STATE MANAGER: edit: toggleSetting(k) { this.progress.settings[k] = !this.progress.settings…

FIND:
```js

  // ---------- settings
  toggleSetting(k) { this.progress.settings[k] = !this.progress.settings[k]; this.saveProgress(); UI.refreshSettings(); },
  changeVolume(d) {
```
REPLACE WITH:
```js

  // ---------- settings
  toggleSetting(k) { this.progress.settings[k] = !this.progress.settings[k]; this.saveProgress(); UI.refreshSettings(); if (k === 'arachnophobia') Crawlers.render(); },
  changeVolume(d) {
```

## PATCH #117 — 12. GAME STATE MANAGER: edit: if (this.mode === 'endless') this.mode = 'story';

INSERT AFTER:
```js
  debugLoadLevel(i) {
    this.stats.running = true;
    this.transition(() => { this.restoreWorld(); this.loadLevel(i, 'PLAYING'); }, 3);
```
NEW CODE:
```js
    if (this.mode === 'endless') this.mode = 'story';
```

## PATCH #118 — 12. GAME STATE MANAGER: every noise reaches the Warden (returns true if it lured it) and the Crawlers.

FIND:
```js
    if (speed > 0.12) AudioSys.impact(surf, point, speed);
    Input.haptic(h.side, clamp(speed / 3, 0.12, 1) * S.haptic * 1.6, 20 + speed * 15);
    if (speed > 0.3 && (this.state === 'PLAYING')) this.noise(point, speed * S.noise);
    if (collider.interact && collider.interact.onTouch) collider.interact.onTouch(h, speed, point);
  },
  noise(pos, loudness) { if (this.state === 'PLAYING') Warden.hear(pos, loudness); },
  onWardenFootstep(pos, strength, silhouette) {
    const d = pos.distanceTo(Player.head);
    if (silhouette) { AudioSys.thud(pos, 2.4); Input.hapticBoth(0.2, 140); return; }
    AudioSys.thud(pos, strength);
    const k = Math.pow(clamp(1 - d / CONFIG.WARDEN.FOOTSTEP_HAPTIC_RANGE, 0, 1), 2) * strength;
```
REPLACE WITH:
```js
    if (speed > 0.12) AudioSys.impact(surf, point, speed);
    Input.haptic(h.side, clamp(speed / 3, 0.12, 1) * S.haptic * 1.6, 20 + speed * 15);
    if (speed > 0.3 && (this.state === 'PLAYING')) this.noise(point, speed * S.noise, 'hand');
    if (collider.interact && collider.interact.onTouch) collider.interact.onTouch(h, speed, point);
  },
  // UPDATE 1: every noise reaches the Warden (returns true if it lured it) and the Crawlers.
  // src 'land' is only for Crawlers; Crawlers ignore their own shrieks.
  noise(pos, loudness, src) {
    if (this.state !== 'PLAYING') return false;
    const lured = src === 'land' ? false : Warden.hear(pos, loudness);
    if (src !== 'crawler') Crawlers.hear(pos, loudness, src);
    return !!lured;
  },
  onWardenFootstep(pos, strength, silhouette) {
    const d = pos.distanceTo(Player.head);
    if (silhouette) { AudioSys.thud(pos, 2.4); Input.hapticBoth(0.2, 140); Subtitles.add('[a distant thud]', pos); return; }
    AudioSys.thud(pos, strength);
    Subtitles.add('[heavy footsteps]', pos, 'wstep');   // UPDATE 1
    const k = Math.pow(clamp(1 - d / CONFIG.WARDEN.FOOTSTEP_HAPTIC_RANGE, 0, 1), 2) * strength;
```

## PATCH #119 — 12. GAME STATE MANAGER: UPDATE 1

FIND:
```js
      const first = !this.progress.toys[this.levelIndex];
      this.progress.toys[this.levelIndex] = true; this.saveProgress();
      this.toast(first ? 'A SMALL CARVED TOY' : 'A SMALL CARVED TOY (again)');
    }
  },
```
REPLACE WITH:
```js
      const first = !this.progress.toys[this.levelIndex];
      this.progress.toys[this.levelIndex] = true; this.saveProgress();
      this.toast(first ? `A SMALL CARVED TOY  (${this.progress.toys.filter(Boolean).length} / 9)` : 'A SMALL CARVED TOY (again)');
      Achievements.checkCollections(); Hub.refreshShelf(); UI.refreshSettings();
    } else if (type === 'gem') { this.toast('A GLOWING STONE'); this.objectiveProgress('stones'); }   // UPDATE 1
  },
```

## PATCH #120 — 12. GAME STATE MANAGER: respawning here puts the water back where it was

INSERT AFTER:
```js
    lantern.respawnPos(this.checkpoint);
    this.checkpointLantern = lantern;
    if (this.state === 'PLAYING') this.toast('LANTERN LIT - PROGRESS SAVED');
```
NEW CODE:
```js
    Water.snapshot(this.checkpointWater);   // UPDATE 1: respawning here puts the water back where it was
```

## PATCH #121 — 12. GAME STATE MANAGER: edit: const names = { valve: 'VALVE', bell: 'BELL', lantern: 'LANTERN', gene…

FIND:
```js
    if (O.type !== kind || O.done) return;
    O.have = kind === 'generator' ? O.need : O.have + 1;   // the generator reports once, when fully powered
    const names = { valve: 'VALVE', bell: 'BELL', lantern: 'LANTERN', generator: 'GENERATOR' };
    if (O.have < O.need) this.toast(`${names[kind]} ${O.have} / ${O.need}`);
```
REPLACE WITH:
```js
    if (O.type !== kind || O.done) return;
    O.have = kind === 'generator' ? O.need : O.have + 1;   // the generator reports once, when fully powered
    const names = { valve: 'VALVE', bell: 'BELL', lantern: 'LANTERN', generator: 'GENERATOR', stones: 'STONE', chapelbell: 'BELL', cord: 'CORD' };
    if (O.have < O.need) this.toast(`${names[kind]} ${O.have} / ${O.need}`);
```

## PATCH #122 — 12. GAME STATE MANAGER: edit: else if (kind === 'chapelbell') this.toast('THE HATCH ABOVE IS OPEN - …

FIND:
```js
      if (kind === 'lantern') { this.toast('SOMETHING OPENED BY THE DRAIN'); this.silhouetteT = 5; }
      else if (kind === 'generator') { this.toast('POWER! THE LIFT IS OPEN'); for (const l of Interact.lamps) l.powered = true; }
      else this.toast('A WAY OUT HAS OPENED');
    }
```
REPLACE WITH:
```js
      if (kind === 'lantern') { this.toast('SOMETHING OPENED BY THE DRAIN'); this.silhouetteT = 5; }
      else if (kind === 'generator') { this.toast('POWER! THE LIFT IS OPEN'); for (const l of Interact.lamps) l.powered = true; }
      else if (kind === 'chapelbell') this.toast('THE HATCH ABOVE IS OPEN - CLIMB!');
      else if (kind === 'cord') this.toast('THE LAST CORD');
      else this.toast('A WAY OUT HAS OPENED');
      if (kind === 'bell') { this.progress.stats.canopyBells = true; this.saveProgress(); Achievements.checkCollections(); }
      if (kind === 'chapelbell') { this.progress.stats.chapelBell = true; this.saveProgress(); Achievements.checkCollections(); }
    }
```

## PATCH #123 — 12. GAME STATE MANAGER: for (const h of Player.hands) if (h.cord) Cords.letGo(h.cord);

INSERT AFTER:
```js
  },
  respawn(fall) {
    Player.placeHeadAt(this.checkpoint);
```
NEW CODE:
```js
    Grab.resetForRespawn(); Crawlers.resetForRespawn(); Notes.hide();   // UPDATE 1
    for (const h of Player.hands) if (h.cord) Cords.letGo(h.cord);
    Water.restoreFog(); Water.restore(this.checkpointWater);
```

## PATCH #124 — NEW SECTION — 12. GAME STATE MANAGER: events

INSERT AFTER:
```js
    if (!fall || Warden.pos.distanceTo(this.checkpoint) < 14) Warden.resetFar(this.checkpoint);
    Dust.clear();
  },
```
NEW CODE:
```js
  },
  // ---------- UPDATE 1 events
  drown() {
    if (this.state !== 'PLAYING') return;
    this.stats.deaths++;
    this.toast('YOU DROWNED');
    this.transition(() => { this.respawn(true); this.state = 'PLAYING'; }, 2);
  },
  onBellRung(kind) {
    if (kind !== 'chapelbell') return;
    Water.startFinal();                 // the final surge: climb!
    Level.triggerStage('bell');
    if (Warden.active && Warden.mode === 'normal') { Warden.lastKnown.copy(Player.head); Warden.hurt(); }
  },
  onCrawlerRemoved() {
    this.progress.stats.crawlersRemoved++;
    this.saveProgress();
    Achievements.checkCollections();
  },
  onWardenHunt() { this.huntedThisLevel = true; },
  playerSlamTarget() {   // the slammable platform you are standing on or holding, if any
    let t = Game.time - Player.groundTime < 0.3 ? this.slamOf(Player.groundCollider) : null;
    for (const h of Player.hands) if (!t && h.anchored) t = this.slamOf(h.collider);
    return t;
  },
  slamOf(col) { return col && col.interact && col.interact.slamPlatform && !col.interact.collapsed ? col.interact : null; },
  onSlam(roof) {
    roof.collapse();
    AudioSys.thud(roof.center, 2); AudioSys.crash(roof.center, 0.8);
    Dust.emit(roof.center, 50, 4, 0x6a5a4a, -0.5, 2.5, 1.2);
    Input.hapticBoth(1, 400);
    Subtitles.add('[CRASH]', roof.center);
    this.noise(roof.center, 4, 'slam');
  },
  onCordCut(c) {
    this.objectiveProgress('cord');
    if (c.opens) Level.triggerStage(c.opens);     // the Heart changes shape after every cut
    Input.hapticBoth(0.8, 800);
    AudioSys.wetCreak(Heart.center, 1); AudioSys.roar(Heart.center, 0.6);
    if (Cords.remaining() > 0) { Warden.hurt(); if (Warden.active && this.mode !== 'timetrial') Crawlers.shed(2, Warden); return; }
    // the last cord: the heart lets go of him
    Achievements.award('trueending');
    Heart.stop();
    if (!(this.mode !== 'timetrial' && Warden.startDying(_uw.fromArray(this.levelData.fallToward || [0, 0, 0])))) this.onWardenFallen();
  },
  onWardenFallen() {
    Level.triggerStage('final');      // the path behind you is crushed; the shaft to daylight opens
    for (const c of Crawlers.list) AudioSys.chitter(c.pos, 0.4);
    Crawlers.clear();                 // the swarm scatters into the walls
    Input.hapticBoth(1, 900);
    this.toast('CLIMB TO THE LIGHT');
    UI.wristKey = '';
  },
  onTrueEnding() {
    this.state = 'OUTRO'; this.outroT = 0; this.stats.running = false;
    this.silence = true;
    const P = this.progress;
    P.endings.true = true; P.endings.first = true; P.unlocked = 8; this.saveProgress();
    Achievements.award('trueending'); UI.refreshSettings();
    AudioSys.startAmbience({ wind: 0.35, windCut: 900, gusts: 0.4 });
    const F = this.scene.fog;
    this.outroFrom = { sky: Level.hemi.color.clone(), ground: Level.hemi.groundColor.clone(), hi: Level.hemi.intensity, fog: F.color.clone(), dens: F.density,
      sun: Level.sun ? Level.sun.color.clone() : null, si: Level.sun ? Level.sun.intensity : 0 };
    this.birdT = 2;
  },
  updateOutro(dt) {   // silence, birds, wind, and a slow sunrise
    this.outroT += dt;
    const k = smoothstep(0, 14, this.outroT), O = this.outroFrom, F = this.scene.fog;
    Level.hemi.color.copy(O.sky).lerp(DAWN.sky, k); Level.hemi.groundColor.copy(O.ground).lerp(DAWN.ground, k);
    Level.hemi.intensity = lerp(O.hi, 1.7 * CONFIG.LIGHT_SCALE, k);
    F.color.copy(O.fog).lerp(DAWN.fog, k); F.density = lerp(O.dens, 0.006, k);
    this.scene.background.copy(F.color);
    if (Level.sun) { Level.sun.color.copy(O.sun).lerp(DAWN.sun, k); Level.sun.intensity = lerp(O.si, 1.5 * CONFIG.LIGHT_SCALE, k); }
    this.birdT -= dt;
    if (this.birdT <= 0) { this.birdT = 1.2 + Math.random() * 2.5; AudioSys.birds(Player.head); Subtitles.add('[birdsong]', null, 'birds'); }
    if (this.outroT > 18 && this.state === 'OUTRO') this.toEndScreen('true', {});
  },
  setSystemsVisible(v) {   // persistent meshes outside the level root (Crawlers, props, ghost)
    for (const k in Crawlers.meshes) Crawlers.meshes[k].visible = v;
    for (const k in Grab.meshes) Grab.meshes[k].visible = v;
    Grab.glow.visible = v && !!Grab.litFlare;
    if (!v) Ghost.group.visible = false;
```

## PATCH #125 — 12. GAME STATE MANAGER: it remembers where it caught you

INSERT AFTER:
```js
    this.state = 'CAUGHT'; this.catchT = 0;
    this.stats.deaths++;
    const reduced = this.progress.settings.reducedScares;
```
NEW CODE:
```js
    // UPDATE 1: it remembers where it caught you
    this.progress.lastCatch[this.levelIndex] = [+Player.head.x.toFixed(1), +Player.head.y.toFixed(1), +Player.head.z.toFixed(1)];
    this.saveProgress();
    Water.restoreFog(); Hiding.overlayK = 0;
```

## PATCH #126 — 12. GAME STATE MANAGER: UPDATE 1

INSERT AFTER:
```js
    Level.hideMeshes(); Warden.root.visible = false; Dust.points.visible = false;
    for (const h of Player.hands) h.visual.visible = false;
    Flashlight.suppressed = true;
```
NEW CODE:
```js
    this.setSystemsVisible(false);   // UPDATE 1
```

## PATCH #127 — 12. GAME STATE MANAGER: one life

FIND:
```js
      if (t > (reduced ? 1.8 : 1.5)) { this.face.visible = false; this.faceLight.intensity = 0; }
    }
    if (t > 1.8 && !UI.message.mesh.visible && t < CONFIG.CATCH_TIME) UI.showMessage('IT FOUND YOU', 'back to the last lantern...', 1.6);
    if (t >= CONFIG.CATCH_TIME) {
```
REPLACE WITH:
```js
      if (t > (reduced ? 1.8 : 1.5)) { this.face.visible = false; this.faceLight.intensity = 0; }
    }
    if (t > 1.8 && !UI.message.mesh.visible && t < CONFIG.CATCH_TIME) UI.showMessage('IT FOUND YOU', this.mode === 'endless' ? `floor ${this.endless.floor}` : 'back to the last lantern...', 1.6);
    if (t >= CONFIG.CATCH_TIME && this.mode === 'endless') { UI.hideMessage(); this.endlessOver(); return; }   // UPDATE 1: one life
    if (t >= CONFIG.CATCH_TIME) {
```

## PATCH #128 — 12. GAME STATE MANAGER: UPDATE 1

INSERT AFTER:
```js
    Warden.root.visible = Warden.active && (Warden.mode !== 'climb' || (Warden.climb && Warden.climb.phase !== 'wait'));
    Dust.points.visible = true;
    Flashlight.suppressed = false;
```
NEW CODE:
```js
    this.setSystemsVisible(true);   // UPDATE 1
```

## PATCH #129 — 12. GAME STATE MANAGER: if (this.mode === 'timetrial') { this.onLevelFinished(); this.finishTimeTrial(); return; }

INSERT AFTER:
```js
  onFinalGate(exit) {
    if (this.state !== 'PLAYING') return;
    this.state = 'ENDING'; this.endT = 0;
```
NEW CODE:
```js
    Achievements.award('escapee');   // UPDATE 1
    if (this.mode === 'timetrial') { this.onLevelFinished(); this.finishTimeTrial(); return; }
    this.onLevelFinished();
```

## PATCH #130 — 12. GAME STATE MANAGER: as it leaves, the ground behind the gate splits open

FIND:
```js
  updateEnding(dt) {
    this.endT += dt;
    if (this.endT > 7 && Warden.phase === 'leave' && this.endT > 12 || this.endT > 22) {
      if (this.fadeTarget === 0 && this.state === 'ENDING') {
```
REPLACE WITH:
```js
  updateEnding(dt) {
    this.endT += dt;
    // UPDATE 1: as it leaves, the ground behind the gate splits open
    if (Crack.t < 0 && (Warden.phase === 'withdraw' || Warden.phase === 'leave' || this.endT > 18)) Crack.start(_uw.set(0, 0.03, -179));
    Crack.update(dt);
    if (Crack.t > 5.5 || this.endT > 32) {
      if (this.fadeTarget === 0 && this.state === 'ENDING') {
```

## PATCH #131 — 12. GAME STATE MANAGER: The Deeper Dark opens

FIND:
```js
          this.scene.fog.color.setHex(0x000000); this.scene.background.setHex(0x000000);
          this.state = 'END';
          this.progress.unlocked = 5; this.saveProgress();
          UI.showEnd(this.stats);
          this.fadeTarget = 0;
```
REPLACE WITH:
```js
          this.scene.fog.color.setHex(0x000000); this.scene.background.setHex(0x000000);
          this.state = 'END';
          this.progress.unlocked = Math.max(this.progress.unlocked, 6);   // UPDATE 1: The Deeper Dark opens
          this.progress.endings.first = true; this.saveProgress();
          UI.refreshSettings();
          UI.showEnd(this.stats, 'first');
          this.fadeTarget = 0;
```

## PATCH #132 — 12. GAME STATE MANAGER: a flare lights you up

INSERT AFTER:
```js
    for (const l of Interact.lamps) { const r = l.light.distance * 0.7, d = _uv.setFromMatrixPosition(l.light.matrixWorld).distanceTo(H); if (d < r) v += 0.5 * (1 - d / r) * (l.light.intensity / l.base); }
    if (Flashlight.on) v += 0.45;
    this.playerLight = v;
```
NEW CODE:
```js
    if (Grab.litFlare) { const d = Grab.litFlare.pos.distanceTo(H); if (d < 9) v += 1.3 * (1 - d / 9); }   // UPDATE 1: a flare lights you up
```

## PATCH #133 — 12. GAME STATE MANAGER: systems

FIND:
```js
        else if (this.silhouetteT < 0 && this.playT > 100) { this.silhouetteT = 0; Warden.startSilhouette(); }
      }
    } else if (S === 'CAUGHT') this.updateCatch(dt);
    else if (S === 'ENDING') { Warden.update(dt); Interact.update(dt); this.updateEnding(dt); }
    Dust.update(dt);
```
REPLACE WITH:
```js
        else if (this.silhouetteT < 0 && this.playT > 100) { this.silhouetteT = 0; Warden.startSilhouette(); }
      }
      // UPDATE 1 systems
      Crawlers.update(dt); Grab.update(dt); Hiding.update(dt); Water.update(dt); Cords.update(dt);
      Hub.update(dt); Notes.update(dt); Ghost.update(dt);
    } else if (S === 'CAUGHT') this.updateCatch(dt);
    else if (S === 'ENDING') { Warden.update(dt); Interact.update(dt); this.updateEnding(dt); }
    else if (S === 'OUTRO') { Interact.update(dt); Grab.update(dt); Notes.update(dt); this.updateOutro(dt); }
    else if (S === 'TRANSITION') Crack.update(dt);
    Heart.update(dt); Subtitles.update(dt);
    Dust.update(dt);
```

## PATCH #134 — 12. GAME STATE MANAGER: const chase = !this.silence && S !== 'CAUGHT' && S !== 'END' && wv && (Warden.state === 'H

FIND:
```js
      else if (Warden.state === 'INVESTIGATE' || Warden.state === 'SEARCH') f += 0.12;
      if (Warden.mode === 'silhouette') f = 0.15;
    }
    if (this.silence || S === 'END' || S === 'CAUGHT') f = 0;
    this.fear = damp(this.fear, clamp(f, 0, 1), 1.5, dt);
    AudioSys.updateLoops(dt, this.fear, Warden.headPos, wv && !this.silence && S !== 'CAUGHT', Warden.breathVol);
    const chase = !this.silence && S !== 'CAUGHT' && S !== 'END' && wv && (Warden.state === 'HUNT' || Warden.state === 'REACH' || (Warden.mode === 'chase' && S === 'PLAYING')) ? 1 : 0;
    const drone = this.silence || S === 'END' ? 0 : (this.levelData && this.levelData.music ? this.levelData.music.drone : 0.5);
    AudioSys.updateMusic(dt, drone, this.silence ? 0 : clamp((this.fear - 0.1) * 1.4, 0, 1), chase);
    AudioSys.updateListener(Player.head, Player.headWorldQuat);
```
REPLACE WITH:
```js
      else if (Warden.state === 'INVESTIGATE' || Warden.state === 'SEARCH') f += 0.12;
      if (Warden.mode === 'silhouette') f = 0.15;
      if (Warden.mode === 'sleep') f = 0.12 + Warden.wake * 0.5;   // UPDATE 1
    }
    if (Player.hands[0].cling || Player.hands[1].cling) f += 0.35;
    if (this.silence || S === 'END' || S === 'CAUGHT') f = 0;
    this.fear = damp(this.fear, clamp(f, 0, 1), 1.5, dt);
    AudioSys.updateLoops(dt, this.fear, Warden.headPos, wv && !this.silence && S !== 'CAUGHT', Warden.breathVol, Warden.breathRate, S === 'PLAYING' ? Hiding.overlayK : 0);
    AudioSys.setMuffle(S === 'CAUGHT' || S === 'END' ? 0 : Math.max(Water.muffle, Hiding.overlayK * U1.HIDE_MUFFLE));   // UPDATE 1
    const chase = !this.silence && S !== 'CAUGHT' && S !== 'END' && wv && (Warden.state === 'HUNT' || Warden.state === 'REACH' || (Warden.mode === 'chase' && S === 'PLAYING')) ? 1 : 0;
    const drone = this.silence || S === 'END' ? 0 : (this.levelData && this.levelData.music ? this.levelData.music.drone : 0.5);
    const descent = this.mode === 'endless' && S !== 'END' ? Math.min(1, this.endless.floor / 10) : 0;   // UPDATE 1
    AudioSys.updateMusic(dt, drone, this.silence ? 0 : clamp((this.fear - 0.1) * 1.4, 0, 1), chase, descent);
    AudioSys.updateListener(Player.head, Player.headWorldQuat);
```

## PATCH #135 — 12. GAME STATE MANAGER: the desktop shake lasts one frame

FIND:
```js
      if (hint.textContent !== txt) hint.textContent = txt;
    }
  },
};

```
REPLACE WITH:
```js
      if (hint.textContent !== txt) hint.textContent = txt;
    }
    Input.shakePulse = false;   // UPDATE 1: the desktop shake lasts one frame
  },
};
const DAWN = { sky: new THREE.Color(0xffc8a0), ground: new THREE.Color(0x6a5a40), fog: new THREE.Color(0xe8b48c), sun: new THREE.Color(0xffa860) };

```

## PATCH #136 — 13. MAIN LOOP: Grab.build(scene);

FIND:
```js
Dust.init(scene);
Warden.build(scene);
Game.init(renderer, scene, camera);
UI.init(scene, camera);
Game.loadLevel(0, 'MENU');
```
REPLACE WITH:
```js
Dust.init(scene);
Warden.build(scene);
Crawlers.build(scene);   // UPDATE 1
Grab.build(scene);
Game.init(renderer, scene, camera);
UI.init(scene, camera);
Subtitles.init(camera); Hiding.init(camera); Water.init(camera); Notes.init(scene); Ghost.init(scene); Cosmetics.init();
Game.loadLevel(0, 'MENU');
```

## PATCH #137 — 13. MAIN LOOP: edit: window.HOLLOWMAW = { frame, THREE, CONFIG, Game, Player, Warden, World…

FIND:
```js
renderer.setAnimationLoop(frame);
// handles for debugging from the browser console
window.HOLLOWMAW = { frame, THREE, CONFIG, Game, Player, Warden, World, Level, Input, AudioSys, UI, Interact, Flashlight, renderer, scene, camera };
document.getElementById('status').textContent = navigator.xr ? 'Ready. Press ENTER VR below, or play on desktop.' : 'Ready. WebXR not available here - desktop debug mode only.';
```
REPLACE WITH:
```js
renderer.setAnimationLoop(frame);
// handles for debugging from the browser console
window.HOLLOWMAW = { frame, THREE, CONFIG, Game, Player, Warden, World, Level, Input, AudioSys, UI, Interact, Flashlight, renderer, scene, camera,
  Crawlers, Grab, Hiding, Water, Cords, Notes, Heart, Ghost, Hub, Achievements, Cosmetics, Subtitles, Store, LEVELS, Crack };
document.getElementById('status').textContent = navigator.xr ? 'Ready. Press ENTER VR below, or play on desktop.' : 'Ready. WebXR not available here - desktop debug mode only.';
```

