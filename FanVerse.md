[Skip to content](#main)

Countdown theater

**00**Hours

**00**Min

**00**Sec

0 in the theater

Locations

Personalization engine

## Your art, your colors

Pick an image of a favorite character or poster. The accent system, glow and 3D scene re-tint to match. The image stays on your device.

Choose image

Using the realm palette

Synced party

In syncmax drift 0 mssimulated room

Reactions float in the room

Fan art studio

## Draw with the room

Brush

Two collaborators are simulated here. The production build syncs strokes over WebSocket with a CRDT, and runs style transfer and upscaling on a server queue.

Hall of Fame

Z

Your profile

### Fan 0417

No relic equipped

Delivery pack

## Blueprint

### Shell and realm packs

- Shell (under 150 KB gzipped): router, tokens, header, dock, service worker. It paints before any 3D loads.
- Each realm is a lazy pack described by a manifest: shaders, KTX2 textures, Opus audio, token set, lore index. The portal animation runs while the next pack streams in, so the 1.2 s switch holds on warm cache.
- Three.js scene manager owns one WebGL context. Realms swap scene graphs, never contexts. Disposal runs on every switch.
- Quality tiers (low, mid, high) picked from a 90-frame frame-time probe: pixel ratio, particle counts, bloom on or off. The prototype already does the first two.

### Real-time systems

- **Studio:** edge WebSocket gateway with one room per canvas, Yjs CRDT for strokes and layers, awareness channel for cursors. Rooms shard by id; snapshots go to object storage every 30 s.
- **Watch party:** server holds the room clock. Clients estimate offset with NTP-style ping rounds, then nudge `playbackRate` within ±4% for drift under 250 ms and hard-seek above that. Target under 100 ms at the 95th percentile.
- **Reactions:** unreliable, unordered messages, batched per frame, rendered in 3D relative to the video plane.
- **Voice:** SFU (LiveKit class). Each speaker feeds a Web Audio `PannerNode` with HRTF, placed at their seat in the room.
- **AI:** all model calls go through a server queue. Style transfer and upscaling stream partial results back over the room socket. The companion is an LLM with per-realm lore retrieval and a session memory window.

### Performance and offline

- Budgets: shell LCP under 1.8 s on mid-range Android, realm pack under 2.5 MB, 60 fps floor.
- Workbox: shell precache, realm packs cache-first with versioned manifests, API stale-while-revalidate.
- Accessibility: full keyboard path, `prefers-reduced-motion` swaps camera moves and particle flow for crossfades and static light, `prefers-contrast` raises panel opacity. Both exist in this prototype.
- Analytics: on-device preference model (realm dwell, tab usage). Only anonymous aggregate counts leave the device.

### Motion principles

| Token | Value | Use |
| --- | --- | --- |
| --dur-fast | 160 ms | hover, press, toggle |
| --dur-base | 320 ms | cards, sheets |
| --dur-scene | 560 ms | tab changes, staggers |
| --dur-portal | 1100 ms | realm switch (hard cap 1200) |
| ease-out | power3.out | entrances |
| ease-in | power3.in | portal opening |

- Every transition has an origin: the portal opens where you tapped, sheets rise from the dock.
- One hero motion per screen. Everything else is ambient and slow.
- Reduced motion keeps color, light and sound changes, and drops travel and parallax.

### Realm theming rules

| Token | Velocity | Encore |
| --- | --- | --- |
| --scene | #060a14 | #0d0616 |
| --accent | #ff4d2e | #ff5fd2 |
| --accent2 | #ffd23f | #8b6cff |
| --font-d | Big Shoulders Display | Syne |
| Scene | speed streaks, grid floor | beams, waveform rings |
| Audio | engine drone, wind | kick, hat, arp |

- A realm sets exactly: scene color, an accent pair, a display face, a scene graph and an audio bed. Nothing else may change, so layout stays learnable.
- Uploaded art overrides only the accent pair.
- Light theme keeps the 3D scene and lays a frosted veil over it; accent text is darkened to hold contrast.

### Components

- Glass card, pill button, dock tab, realm switch, countdown cell, room tile, relic card with pointer tilt, emote, cursor tag, companion bubble.

**Phase 1 · Immersive shell (weeks 1–6)**

Shell, realm pack loader, portal, two realms, personalization, PWA, accessibility modes, countdown theaters. This prototype is the design target.

**Phase 2 · Social core (weeks 7–12)**

Accounts, community locations with persistent chat, event radar with real schedules, relic ownership and profiles.

**Phase 3 · Live rooms (weeks 13–20)**

Synced watch and listen parties, spatial voice, 3D reactions, load testing to 5k per room.

**Phase 4 · Creation (weeks 21–28)**

Collaborative canvas on CRDT, AI style tools, Hall of Fame, moderation pipeline.

**Phase 5 · AR and scale (weeks 29+)**

WebXR placement with Quick Look fallback on iOS, more realms, licensing partnerships.

### Where the brief needs a decision

- **Refraction and bloom:** true refraction on every panel costs too much on mid-range phones. Proposal: backdrop blur everywhere, SVG displacement on high tier only, bloom faked with additive sprites.
- **AR:** WebXR is patchy on iOS Safari. Proposal: WebXR where present, USDZ Quick Look elsewhere.
- **Sub-100 ms sync:** achievable on broadcast streams you control. Third-party embeds can't be nudged. Proposal: partner streams or user-supplied files first.
- **Fandom IP:** named franchises need licenses. Proposal: launch with original realms like these two, then add licensed realms case by case.
- **AI cost:** style transfer on every stroke is expensive. Proposal: run on release, with a per-user daily quota.

### What this prototype fakes

- The room, drift readings, collaborators, chat crowd and companion replies are simulated in the browser.
- AR and camera features are not available inside a preview.
- Audio is synthesized on device, not licensed music.

Choose your realm