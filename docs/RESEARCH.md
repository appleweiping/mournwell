# Research and design evidence

Research was used to understand genre-level rules and current library APIs—not
to extract or reproduce another game's assets, text, room data, balance tables,
characters, or presentation. The implementation translates those principles
into an original bell-and-well folk-horror setting.

## Firecrawl discovery log

Firecrawl CLI 1.19.27 was used on 2026-08-02. The account was authenticated and
each search returned a durable result identifier.

| Topic             | Exact query                                                                                     | Result ID                              | Representative sources                                                                                                                                                                         |
| ----------------- | ----------------------------------------------------------------------------------------------- | -------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Floor topology    | `The Binding of Isaac room layout generation rules normal treasure boss rooms floor generation` | `019fc30b-7155-746c-a733-360dfcbe3253` | [Level Generation](https://bindingofisaacrebirth.fandom.com/wiki/Level_Generation), [BorisTheBrave analysis](https://www.boristhebrave.com/2020/09/12/dungeon-generation-in-binding-of-isaac/) |
| Enemy readability | `The Binding of Isaac enemy AI patterns chase shoot charge telegraph design`                    | `019fc30b-e901-7625-94e7-854aa08d52a7` | [Gaper reference](https://bindingofisaacrebirth.wiki.gg/wiki/Gaper), [Bestiary](https://bindingofisaacrebirth.wiki.gg/wiki/Bestiary)                                                           |
| Items and synergy | `The Binding of Isaac item design stat upgrades stacking synergies tears damage range speed`    | `019fc30b-7615-75eb-a616-ece90cd12fd8` | [Items overview](https://bindingofisaacrebirth.fandom.com/wiki/Items), [community item reference](https://tboi.com/)                                                                           |
| Visual language   | `Edmund McMillen Binding of Isaac visual style interview dark cartoon hand drawn`               | `019fc30b-e522-723b-9653-68c9c9cf3f97` | Creator interviews indexed by GeekGeneration and Postgame                                                                                                                                      |

Design conclusions retained at the genre level were: compact cardinal room
graphs make navigation legible; combat silhouettes need distinct movement and
telegraph rhythms; rewards feel meaningful when they alter both numbers and
attack behavior; and a dark palette still needs warm focal accents and strong
contrast. MOURNWELL's graph constraints, exact values, cast, names, UI, art, and
audio were then authored independently.

## Context7 API verification

The latest Context7 MCP server available at implementation time reported version
3.2.5. Library resolution selected the high-reputation Phaser documentation ID
`/phaserjs/phaser/v3_90_0`.

Queries covered:

1. Arcade Physics top-down velocity, groups, collision callbacks, world bounds,
   projectiles, keyboard input, pointer coordinates, and cameras.
2. Simultaneous pointer handling with `activePointers`, `addPointer`, pointer
   IDs, `isDown`, active state, and world coordinates.

Primary returned references included Phaser's Arcade Physics skill/documentation,
`BaseCamera.js`, `ArcadePhysics.js`, `Pointer.js`, and release changelogs. These
checks informed velocity handling, camera transforms, independent touch pointer
ownership, and the tested Phaser 3.90 API surface. See the [Phaser
documentation](https://docs.phaser.io/), [Phaser source](https://github.com/phaserjs/phaser),
and [Context7 documentation](https://context7.com/docs) for the upstream APIs.

## IP boundary

- No source-game asset, audio, font, name, story, UI image, map, or item table is
  stored or loaded.
- All production visuals are runtime Graphics/Canvas/CSS/SVG instructions; all
  sounds are runtime oscillators/noise envelopes.
- The project uses only broad, unprotectable genre mechanics such as room
  clearing, directional projectiles, procedural connected spaces, stat upgrades,
  and a final encounter.
- The MOURNWELL name and commercial storefront availability still require
  jurisdiction-specific trademark clearance before monetization.

Research results can change or disappear; the query text and result IDs are kept
here so the discovery process remains auditable even if a source URL moves.
