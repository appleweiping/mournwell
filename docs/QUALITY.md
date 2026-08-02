# Quality and verification

Release 1.0.0 was built in five playable increments. Each increment ended with
real browser interaction and a visual readback before the next system was added.

## Iteration record

| Iteration     | Playable slice                                                 | Verification focus                                                 |
| ------------- | -------------------------------------------------------------- | ------------------------------------------------------------------ |
| 1 — chamber   | One code-drawn room, movement, four-way cast, one enemy        | Input responsiveness, collisions, HP and projectile snapshots      |
| 2 — floor     | Seeded 5–8 room graph, transitions, sealed/open doors, minimap | Reachability, reciprocal doors, room persistence                   |
| 3 — build     | Rewards, chests, eight stackable relics, live stat panel       | Real movement pickup, inventory/HUD/stat agreement, formula tests  |
| 4 — run       | Three normal enemies, three-phase Boss, death/victory results  | Damage, kill, door-open, death and Boss journeys                   |
| 5 — hardening | Mobile dual touch, pause, save validation, CI and docs         | Simultaneous CDP touch, console/network checks, visual breakpoints |

## Automated evidence

Run the release gate from a clean checkout:

```bash
npm ci
npx playwright install chromium
npm run test:all
npm run audit:prod
```

| Layer           | Current coverage                                                                                                                                         |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Unit            | Seed repeatability, stream independence, item stacking, caps/floors                                                                                      |
| Property        | 10,000 generated dungeon seeds validate topology and special-room invariants                                                                             |
| Desktop E2E     | Real keyboard move/cast, projectile creation, damage, enemy death, kill accounting, door unlock, movement pickup, HUD/stat mutation, death, Boss victory |
| Mobile E2E      | Emulated iPhone 13 viewport with two simultaneous CDP touch contacts; move and cast together, then stop on release                                       |
| Runtime hygiene | Every browser journey fails on page errors, error-level console output, or failed requests                                                               |
| Static          | TypeScript project references in strict/no-emit mode; ESLint with zero warnings; Prettier check                                                          |
| Supply chain    | Reproducible `npm ci`, official npm registry lock URLs, production audit, Dependabot, CodeQL                                                             |

The demo images in `screenshots/` are generated from seeded QA fixtures in the
same Playwright suite. This makes the README gallery reproducible instead of a
separate hand-staged artifact.

## Manual visual review

The 1440×900 desktop and 390×844 mobile captures are read back after generation.
The review checks hierarchy, player/enemy silhouette separation, projectile and
door legibility, Boss health visibility, result completeness, touch target
spacing, safe-area behavior, and the absence of transient debug/toast overlays.

### External completion benchmark

The user-provided [YISA / The Binding reference](https://yisa.codefather.cn/) was
rendered independently at 1440×900 and an iPhone 13 viewport. It was used only
as a completion benchmark: immediate title hierarchy, an obvious start action,
controls visible before play, large touch targets, and an explicit mobile
orientation strategy. No source, asset, layout code, name, or copy was reused.
MOURNWELL keeps those product-level standards while providing its own identity,
responsive portrait gameplay instead of a rotate-only fallback, accessible DOM
status, deterministic diagnostics, and automated desktop/mobile journeys.

## Release acceptance

- All commands in the release gate exit successfully.
- The production bundle contains no QA mutation API.
- Every required game phase is reachable through player-facing input.
- The same seed regenerates topology, encounters, and rewards.
- No downloaded art/audio asset or source-game IP is shipped.
- GitHub Actions completes before the release tag is created.

## Tested scope and honest limits

Automated browser verification targets current Chromium on a desktop viewport
and Chromium's iPhone 13 emulation. The layout supports modern Firefox and
Safari APIs, but those engines and physical iOS/Android devices are not claimed
as certified for 1.0.0. Frame pacing can vary with GPU/browser power policy. A
paid distribution should add a physical-device matrix, accessibility testing
with assistive technology, localization, controller certification, legal name
clearance, store compliance, and longer soak/performance profiling.

The shipped build has no telemetry, backend, user accounts, multiplayer, cloud
save, monetization, or user-generated content. Those omissions substantially
reduce the current attack and privacy surface; introducing any of them requires
new tests and operational controls.
