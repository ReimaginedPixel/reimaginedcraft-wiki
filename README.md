# ReimaginedCraft Wiki (data)

Structured, player-facing data for the **ReimaginedCraft** Minecraft network:
currencies, items, GUIs and systems (ranks, friends, parties, levels, tags,
the bag, cosmetics, quests, the daily chest and more). This is a **data
repository**, not a rendered site — plain JSON plus the real in-game icons,
meant to be consumed by a frontend (the network's own website, a Discord bot,
whatever needs it) rather than read as prose.

**Current scope:** the **Hub** and **Diamond Trophy** servers only. Other
parts of the network (Limbo, Elevator Chaos, the unreleased custom Rooms
feature) aren't covered yet.

## Structure

```
data/
  manifest.json              index of every data file below
  currencies.json
  ranks.json
  meta/servers.json          network overview + which systems are network-wide vs per-server
  systems/                   how a system works: friends & parties, levels & achievements,
                              tags, the bag, cosmetics & the crafting altar, the quest board,
                              the daily chest, materials & rarity, Diamond Trophy gameplay
  items/                     catalogues: bag items, crates & keys, cosmetics, gathering
                              materials, Diamond Trophy items
  guis/                      menu-by-menu breakdowns (Hub GUIs, Diamond Trophy's FistWatch)
assets/
  icons/<file-id>/<entry-id>.png   real in-game textures, one per documented item/currency/etc.
```

Every data file is one JSON object. Most share a loose common shape:
`id`, `title`, `scope` (`network` / `hub` / `diamondtrophy`), `summary`,
`how_it_works`, `how_to_access`, and one or more of `entries[]` / `guis[]` —
see `data/manifest.json` for the full file list and `icon_convention`.

## Icons

Every `icon` field points to a **real texture pulled from the live resource
packs** — nothing here is AI-generated. An entry without an `icon` field only
has an `icon_hint` (a short text description) because no matching in-game
texture exists yet.

## Accuracy

This data was built by reading the actual plugin source/config, not by
guessing, and cross-checked for internal consistency. It still reflects a
point in time — `open_questions` arrays throughout note anything that
couldn't be confirmed or that looked unfinished/WIP in the live game
(e.g. the in-game store isn't built yet, some cosmetic slots may not be
equippable). It **will drift** as the game changes; treat a stale-looking
entry as a bug to report, not as ground truth.

## What's deliberately excluded

No server addresses/ports, database or credential info, internal permission
nodes, admin/moderation commands, or anything else that isn't meant to be
public. This repo is safe to keep public; the servers' own source repos are
not.

---

© ReimaginedCraft. Game content, names and art belong to the network: feel
free to read/use this data (e.g. via the GitHub API) for tools and sites
about ReimaginedCraft, but it isn't a general-purpose asset pack.
