# MASTER PROMPT — Original Underwater Exploration Game (Single-File Browser Showcase)

## ROLE & MISSION

You are an elite game developer and technical artist. Build a complete, polished, visually stunning first-person underwater exploration game that runs in the browser. It is inspired by the underwater-survival *genre* but is an entirely original work.

This game will be featured in a YouTube video, and your output will be directly compared on camera against another AI agent given this exact same prompt. You will be judged on four things, in this order:

1. **Visual beauty** — it must look breathtaking in every frame.
1. **Smoothness** — rock-solid 60+ FPS at 1080p in Chrome.
1. **Fun and game feel** — movement, scanning, and the sub must feel great.
1. **Reliability** — one complete 3–4 minute playthrough must work flawlessly, every time.

Make this the best-looking browser game you have ever produced.

-----

## IMMERSION FIREWALL (critical — applies to every section below)

Everything in this document is build guidance for YOU. None of it may surface inside the game. The finished product must feel like a real, commercially released game that has no idea it was built from a prompt.

- **Zero meta text anywhere in-game:** no references to YouTube, videos, recording, showcases, viewers, comparisons, AI agents, prompts, Three.js, FPS, performance targets, “demo,” “tech demo,” or any constraint written here. This applies to the start screen, loading text, HUD, objectives, pause menu, databank entries, companion dialogue, end screen, button labels, and every other string the player can see.
- **All in-game text is diegetic** — written from inside the game’s fiction. The companion is a character in the story, never a narrator of the development process.
- **No tutorial pop-ups, tip banners, or instructional toasts** (“TIP: Press Shift to dash!”). The only instructional text permitted anywhere on screen: the single objective line and the small contextual interaction prompts defined in the HUD section. Nothing else.
- **Features never announce themselves.** The HUD-hide key, debug overlay, and camera toggle simply appear in the pause-menu controls list like in any real game — never advertised during play.
- The end screen says only what a real game would say (title, stats, “Thanks for playing,” Continue) — never “thanks for watching” or anything addressed to an audience.

-----

## DELIVERABLES

- `index.html` — the entire game in a single file.
- `README.md` — under one page: how to run, full controls list, quality settings note.
- Nothing else. No FEATURES.md, no TODO files. Spend your effort on the game.

-----

## HARD TECHNICAL CONSTRAINTS (non-negotiable)

1. **Single file.** The entire game lives in one `index.html`. It must run by double-clicking the file in Chrome on Windows (`file://` protocol). No dev server, no build step, no bundler. Verify your CDN imports actually work from `file://`.
1. **Allowed external code:** Three.js and its official addons (EffectComposer, render passes, etc.) loaded from a CDN (jsdelivr or unpkg) via an import map, using a recent stable version you are confident exists. **Nothing else.** No other libraries, no frameworks.
1. **Zero external assets.** No model files, no texture files, no audio files, no image files, no external fonts (system font stack only, or canvas-drawn text). Everything is procedural: geometry built in code, textures generated on `<canvas>`, all audio synthesized with the WebAudio API.
1. **Performance floor: 60+ FPS at 1080p fullscreen** in Chrome on a typical gaming PC, in every zone, on the default quality. If any feature threatens this, reduce particle counts, shadow quality, or effect resolution **before** sacrificing the core look. Use instancing for fish/particles/flora, merged geometry, fog-based culling (only the current zone renders heavily), and cheap or faked shadows.
1. **Quality presets:** Low / Medium / High in the pause menu (default High), switchable live. They scale particles, bloom, shadows, and draw distance.
1. **Determinism:** use a fixed random seed everywhere. Every run must be identical — same spawns, same creature paths, same events. No randomness that could ruin a recorded take.
1. **Debug overlay** on F3 (hidden by default): FPS, frame time, draw calls, triangle count.
1. **Zero console errors.** Handle window resize, pointer-lock loss, and tab-out (auto-pause) gracefully.
1. **Start screen:** “Click to begin” — required to enable pointer lock and resume the WebAudio context. Show the game title here.

-----

## VISUAL STYLE

**Stylized-but-beautiful.** Saturated, painterly, clean readable silhouettes, strong distinct color identity per zone. Do not attempt photorealism — aim for gorgeous.

**Required postprocessing stack (mandatory, this is the soul of the game):**

- Bloom, strong on emissive materials
- Depth-based fog with a per-zone color
- Vignette
- Filmic color grading
- God rays / volumetric light shafts in sunlit water
- Subtle chromatic aberration

**Required underwater atmosphere:**

- Animated caustics on the seafloor in sunlit areas (procedural shader or scrolling canvas texture)
- Drifting particulate “marine snow” everywhere, density per zone
- Light absorption with depth: turquoise → deep blue → black-purple
- **Snell’s window**: looking up near the surface must show the bright circular window of refracted sky with rays — make this shot gorgeous, it will be filmed
- Gentle camera sway while swimming; flora that sways in gentle current (cosmetic current only — nothing pushes the player)
- The water surface seen from below must look beautiful (animated, light-scattering)

No day/night cycle. Each zone has hand-tuned, controlled lighting so every camera angle looks good at all times.

-----

## WORLD LAYOUT

One seamless connected map, experienced as four showcase zones plus two structures. Zones connect through natural funnels (cave mouths, crevices, a trench lip) and fog conceals distant zones so only one renders heavily at a time.

1. **Sunlit Reef** (0–40m): turquoise tropical water, coral formations in pinks/oranges with neon alien accent flora, caustics, fish schools, god rays. The beauty-overload opener.
1. **Glowing Caves** (40–80m): dark winding caverns lit almost entirely by bioluminescent growths (cyan/magenta), drifting glow jellies, thin light shafts through ceiling cracks.
1. **The Blight** (80–120m): eerie infected zone — sickly green-yellow fog, twisted dead coral, pulsing infected nodes, scavenger creatures. Unsettling, beautiful in a wrong way.
1. **Abyss Trench** (120m → 250m+): a vast vertical drop into near-black blue-purple darkness, dense drifting bioluminescent points, a few faint red glowing vents for contrast, and an ancient alien **monolith** glowing on the trench floor. Home of the leviathan.

**Structures:** a small prebuilt habitat base at the reef edge, and a damaged one-person scout sub resting on a sand shelf near it.

Invent original names for every zone, creature, and item. Example flavor only (you may not copy these, invent your own in this spirit): “Glass Reef,” “Trench Titan,” “Deep Lens.” The game’s *title* is the one exception — it’s a parody pun (see Copyright & Originality).

-----

## THE GOLDEN PATH (the 3–4 minute showcase run)

Design the game so a first-time player, simply following the on-screen objectives, naturally experiences this exact sequence. Soft-scripted: objectives, waypoints, and triggered events — not literal rails. The player can swim freely at all times.

- **0:00** — Player floats at the calm surface in golden light. Title card fades out. AI companion text delivers a one-line hook. Objective: *Dive to the reef.*
- **0:15** — The dive: caustics, fish schools, god rays. Objective: *Scan 3 reef lifeforms* (hold E, ~2s each, scan-ring UI). Glowing resource pickups are placed directly along this path.
- **1:00** — Objective: *Return to the habitat.* Inside: fabricator. Craft **Headlamp** + **Scanner Amplifier** (instant — resources were collected en route).
- **1:20** — Objective: *Investigate the signal in the caves.* Headlamp + bioluminescence showcase. Scan the glow jelly and the scavenger.
- **1:50** — Objective: *Sample the Blight.* Scanning an infected node unlocks the **Depth Module** recipe. The territorial predator makes one scripted threatening pass; a thrown flare repels it (teach moment, low stakes).
- **2:10** — **Blackout beat:** returning toward the base, the power fails. Interior lights die, alarm hum, AI companion: a clipped warning. Something massive glides past the big viewport — silhouette and a deep roar only. Player restores power at a wall panel (hold E). This is the act-two hook; make it cinematic.
- **2:30** — Objective: *Repair the scout sub.* Craft **Power Cell**, **Depth Module**, and **Deep-Scan Beacon** at the fabricator; install the two parts at the sub (two short hold-E interactions). Enter the sub (F).
- **2:45** — Descend the trench. Headlights on, pressure creaks, depth readout climbing, bioluminescent specks streaming past the canopy. Distant leviathan reveal: a huge silhouette circling through the fog.
- **3:10** — At the monolith: exit the sub (exiting tops oxygen to full), hold E at the monolith base to deploy the beacon, then survive a ~20-second scan channel while the leviathan circles closer with each pass. The player scans the leviathan itself during a pass for its databank entry. Tension comes from music, proximity, and roars — not real danger.
- **3:30** — Scan completes; the monolith ignites with light. AI companion delivers a short revelation line. Objective: *RETURN TO THE SURFACE.* The leviathan charges — scripted chase back up the trench in the sub: it lunges near-miss close behind, but is choreographed to never actually catch a player who keeps moving forward. If the player stalls, it circles wide rather than killing them. Cosmetic hull alarms scream.
- **3:50** — Breach into sunlit water → **Mission Complete screen**: the game title, stats (lifeforms scanned X/10, max depth reached, time), “Thanks for playing,” and a *Continue Exploring* option that returns to free-roam with everything unlocked.

-----

## PLAYER MECHANICS

- First-person, pointer lock. **WASD** swim + mouse look, **Space** ascend, **Ctrl** descend, **Shift** = jet-dash (speed burst with short cooldown, FOV kick, bubble trail).
- **Oxygen:** ~90 seconds capacity; refills instantly at the surface, in the base, and in the sub. Below 20%: heartbeat audio + screen-edge effect. At 0: quick fade and gentle respawn at the base **keeping all items and progress**. A recording must never be ruined.
- **Health:** exists for drama only. Predator hits cause screen shake and a red vignette flash. At 0: the same gentle no-penalty respawn. It should be nearly impossible to die on a normal run.
- **No hunger, no thirst.**
- **Quickbar tools (1–3):** Scanner, Headlamp (toggle), Flare (throwable glowing light that repels the predator).

-----

## CREATURES & SCANNING

All procedural geometry, all original names and designs. Roughly **10 scan targets**: 6 creatures + 2–3 flora + the monolith. Each scan adds a short, original databank entry (readable from the pause menu). Scanning specific sets unlocks recipes — progression is welded to scanning.

1. **Fish schools** — instanced, simple flocking, scatter from the player. Reef.
1. **Glow jellies** — drifting, pulsing emissive. Caves.
1. **Manta-like glider** — large, peaceful, graceful spline patrol over the reef. The majesty shot.
1. **Crab-squid scavenger** — skittering in the Blight.
1. **Territorial predator** — mid-size; circles and makes bluff charges near the Blight and cave edges; repelled by flares; deals minor damage at most.
1. **Leviathan** — enormous. **Scripted only:** spline patrol paths plus event triggers (head tracks the player, roars at trigger distances, blackout flyby, monolith circling, chase). Do **not** build free-swimming physics/AI for it. Scripted looks identical on camera and never breaks. Sell its scale with sound, slow movement, and fog reveals.

-----

## CRAFTING

Fabricator UI at the base. **Six recipes, instant craft, zero grind:** Headlamp, Scanner Amplifier (faster scans, longer range), Flare ×3, Power Cell, Depth Module, Deep-Scan Beacon. Resources are glowing pickups placed directly on the golden path — the player should never have to search or farm.

-----

## BASE & SUB

**Base (prebuilt):** small habitat with an entry airlock, fabricator, oxygen refill, soft interior lighting and hum, and one **large viewport window facing open water** — this window is the stage for the blackout silhouette beat.

**Sub (found damaged, repaired via the two crafted parts):**

- First-person cockpit with HUD: depth, hull, power; **L** toggles headlights.
- **V** toggles a third-person follow camera (for cinematic exterior shots of headlights cutting the dark).
- Without the Depth Module: warning + auto-stop below 120m. With it: full depth.
- Moves moderately faster than swimming; banks and pitches smoothly; controls feel weighty but responsive.
- Chase alarms and shake are cosmetic.

-----

## HUD / UI

Minimalist, semi-transparent, original sci-fi styling (do not imitate any existing game’s UI).

- **Top center:** current objective, one line, with progress count (“Scan reef lifeforms — 1/3”).
- **One waypoint marker** for the current objective only; it fades out within ~10m so it never pollutes close-up shots.
- **Bottom:** oxygen bar, depth meter, small health indicator, 3-slot quickbar.
- Thin compass strip at top. Scan ring appears only while scanning.
- Contextual prompts only: “[E] Scan”, “[F] Enter Sub”, “[Hold E] Restore Power” — small, fading, near the crosshair. Nothing else instructional ever appears during gameplay: no tip banners, no tutorial pop-ups, no key-reminder overlays.
- **H** hides the entire HUD instantly (list it in the pause menu as “Photo Mode” — never explained on screen during play).
- **Esc** = pause menu: resume, full controls list, quality preset, audio sliders (master/music/SFX), databank, restart. **No controls overlay during gameplay** — controls live only in the pause menu and README.
- **AI companion:** subtitled text lines, bottom center. Voice: calm, mysterious, occasionally dry. Short lines. No memes, no fourth-wall jokes, no exclamation-point enthusiasm.

-----

## AUDIO (all WebAudio-synthesized, no files)

Underwater ambient bed (filtered noise, slow LFO movement), bubble sounds, scan tones + success chime, distinct creature calls (the leviathan roar = layered low synthesized growl with real sub-bass), sub engine hum and sonar ping, low-oxygen heartbeat, alarm, and simple atmospheric generative music layers that shift per zone, with a stinger for the blackout and a driving pulse for the chase. Mix it: ambience quiet, events loud, roar terrifying.

-----

## COPYRIGHT & ORIGINALITY (mandatory)

Inspired by the underwater-survival genre — but you must **not** use Subnautica’s (or any existing game’s) creature names, item names, UI design, story, dialogue, logos, audio, or assets in any form. Every name, design, and line of writing inside the game must be original.

**The one exception is the title:** give the game a comedic PARODY title — obvious wordplay riffing on “Subnautica” that nobody could mistake for the real game. Invent your own pun; it must not be “Subnautica” or “Subnautica 2” verbatim. The parody stops at the title screen: all zones, creatures, items, dialogue, and story stay fully original. Display the title on the start screen and the Mission Complete screen, played completely straight — the game itself never winks at the joke.

-----

## WORKFLOW (follow in order)

1. **Plan** (brief): scene structure, systems list, zone layout, event/trigger timeline for the golden path.
1. **Implement** the complete game.
1. **Self-test:** zero console errors; play the full golden path start to finish and verify every objective, event, craft, and the ending fire correctly; check FPS with your F3 overlay in all four zones and optimize until 60+ is solid.
1. **Polish pass A (mandatory):** water, lighting, postprocessing — push the beauty as far as performance allows.
1. **Polish pass B (mandatory):** game feel — camera sway, dash kick, scan feedback, UI fade animations, audio mix, event timing, transition smoothness.
1. **Secret:** hide ONE small original secret somewhere visible from the golden path. It must be non-blocking, unable to ruin a recording, and not a jump-scare. Do not document what it is anywhere. Let it be found.

-----

## ACCEPTANCE CHECKLIST (verify every item before you finish)

- [ ] Double-clicking `index.html` in Chrome runs the game with zero console errors
- [ ] Solid 60+ FPS at 1080p on the default (High) preset in all four zones, including the chase
- [ ] The golden path is completable in 3–5 minutes by a first-time player just following objectives
- [ ] All ~10 scan targets work and have readable original databank entries
- [ ] All 6 recipes craft; sub repair, depth gate, and full descent work
- [ ] Blackout beat, leviathan reveals, beacon scan, chase, and Mission Complete screen all trigger reliably
- [ ] Runs are deterministic (fixed seed) — identical every time
- [ ] H hides HUD, F3 shows debug, V toggles sub camera, quality presets switch live
- [ ] Oxygen/health can never hard-fail a run (gentle respawn, progress kept)
- [ ] Zero copyrighted names, designs, or assets; parody title displayed; every other name original
- [ ] Zero meta text in-game: nothing about YouTube, recording, AI, prompts, FPS, or any build constraint — every player-visible string is diegetic, and the only instructional text is the objective line + contextual prompts
- [ ] README.md exists with run instructions and the full controls list

Build it.
