---
publish: true
type: reference
tags:
  - reference
---

# How This Vault Works

A map of the map — read this if you're a new player joining, or if it's been six months and you've forgotten your own system. Rewritten 2026-09-21 to match the vault as it actually is, not as it was when first set up (see [[z_Archives/How This Vault Works|the old version]] if you ever need the history).

## Folder Structure

- **Player Characters/\<Name>/** — one folder per PC (`Alvar`, `Hilda`, `Mophlin`, `Willow`). The file named after the character (e.g. `Hilda Trueshield.md`) is the canonical sheet; `Inventory.md` holds their gear; `Reference Images/` holds portrait variants.
- **Personal Notes/** — cross-character material that doesn't belong to one PC folder: `Goals/` (personal goal threads), `Backstory/`, `Scratchpad/` (raw session capture), `Journal/` (in-character journal entries).
- **NPCs/**, **Items/**, **Groups/**, **Bestiary/** — one note per real thing. Deities live as sections inside `z_5.5e Compendium/Deities.md` instead of individual files (see below) — don't recreate the old per-deity page pattern.
- **Locations/** — one note per place, organized into region subfolders (`Phandalin/`, `Neverwinter/`); an underscore-prefixed `_<Region> Overview.md` sits at the top of each subfolder.
- **History/** — `Conflicts/`, `Historical Figures/`, `Stories/`, `Time Periods/` for lore predating the campaign. Empty until something needs writing there.
- **Session Notes/** — `Session N.md` is the recap; `Encounters/`, `Quests/`, `Rumors/`, `Loot/` hold anything spawned mid-session.
- **z\_5.5e Compendium/** — the full 2024 D\&D ruleset (Classes, Character Origins, Feats, Spells, Magic Items, Monsters Library) plus the campaign's own `Deities.md`. Bulk rules text lives here in full; other pages should link into it, not duplicate it.
- **z\_Reference/** — world and rules facts that don't belong to one session: the Calendar, Coinage, Conditions, Glossary, Rules Quick Reference, per-species quick-reference pages (`Races/`), and the five compendium indexes (Class, Feat, Species, Spell, Magic Item) plus the Monster Index.
- **z\_templates/** — the actual templates, organized by category (`Groups/`, `Items/`, `Locations/`, `Combat/`, `Events/`, `Other/`, `CallOuts/`). Never edit an instance file expecting it to update the template, or vice versa. `CallOuts/` are a different kind of template — snippets meant to be _inserted into_ an existing note via Templater, not used to create a new one.
- **Indexes/** — auto-generated overview pages (NPCs Index, Party Roster, Quest Board, Locations Index, Items Index, Groups Index, Loot and Treasury, Character Gallery, Faction Reputation, Ownership, Publish Readiness, The Story So Far, Unfilled Fields). These pull from tags and frontmatter properties automatically; don't hand-edit their Dataview/DataviewJS tables — edit the source note's properties instead.
- **z\_Archives/** — retired material kept for history, not for active reference.
- **z\_miscImgs/** — loose pasted images referenced from notes that don't have their own dedicated image folder.

## Creating New Notes

Use **QuickAdd** (ribbon icon, or Command Palette → "QuickAdd: Run QuickAdd") for anything that has a choice there — as of this rewrite, every template in `z_templates/` has a matching QuickAdd choice except the `CallOuts/` snippets. QuickAdd drops the note in the right folder automatically and links it back into whatever note is open.

For a `CallOuts/` snippet: open the note you're writing in, place your cursor, and use Templater's "Insert Template" command instead — these aren't meant to become their own files.

## The Tag System

Every real note carries an entity-type tag matching its `type:` frontmatter property. Templates additionally carry `#template`, which is **stripped automatically** the moment a note is properly created from one (via Templater or QuickAdd — not copy-paste). Full current list:

| Tag | Used for | Subtags |
| --- | --- | --- |
| `#pc` | Player characters | — |
| `#party` | The party as a single collective entity — see below | — |
| `#npc` | Non-player characters | — |
| `#location` | Places | `location/city`, `location/shop`, `location/temple`, `location/residence`, `location/point-of-interest` |
| `#item` | Items and gear | `item/weapon`, `item/protection`, `item/clothing`, `item/accessory`, `item/gear`, `item/other` |
| `#group` | Factions, orgs, families | `group/commerce`, `group/criminal`, `group/family`, `group/government`, `group/military`, `group/religion`, `group/other` |
| `#bestiary` | In-play field notes on a creature (lore/tactics, not stats — the stats live in the compendium) | — |
| `#companion` | Animal companions, familiars, summons tied to a PC | — |
| `#hazard` | Traps, environmental hazards, curses — anything dangerous that isn't a creature | — |
| `#quest` | Quests | — |
| `#combat` / `#combat-summary` | Combat encounters and their post-fight recap | — |
| `#roleplay` / `#roleplay-summary` | Roleplay scenes and their recap | — |
| `#incident` | Notable non-combat, non-roleplay events worth a record | — |
| `#rumor` | Unconfirmed leads and hearsay | — |
| `#goal` | Personal PC goals | — |
| `#downtime` | Downtime activities | — |
| `#house-rule` | Table-specific rule variants | — |
| `#session` | Session recaps | — |
| `#journal` | In-character journal entries | — |
| `#backstory` | PC backstory pages | — |
| `#scratchpad` | Raw, unedited session capture | — |
| `#race` | Species/lineage quick-reference pages | — |
| `#reference` | Compendium and world-fact pages | — |
| `#index` | Auto-generated overview pages | — |
| `#pantheon` | Deity-related reference pages | — |
| Historical: `#historical-figure`, `#historical-story`, `#historical-period`, `#historical-conflict` | Lore predating the campaign | — |

Deities are the one exception to "one note per real thing": they're sections inside `z_5.5e Compendium/Deities.md` (tagged `#reference`/`#pantheon` at the file level) rather than separate `#npc`/`#group`-style notes, because a deity isn't a thing the party interacts with directly the way an NPC or location is.

## Why Some Table Cells Are Special

Cells that look like `` `INPUT[...]` `` are live **Meta Bind** fields — clicking them gives you a dropdown, toggle, or slider, and typing in one _actually writes to that note's properties_ rather than just being decorative text. Blocks fenced with `dataview` or `dataviewjs` are live queries — they render a table computed from every note's properties at read time, so the Indexes and NPC/Quest cross-references auto-populate without manual upkeep. `DataviewJS` specifically needs its own setting enabled (Settings → Dataview → "Enable DataviewJS queries", off by default) — a few pages need it (Unfilled Fields, the NPCs Index's Active Quests column).

## Ownership

Anything that can belong to someone — Items, Companions, Residences (as a distinct `owner` property from `resident`, since a property can be owned without the owner living there), and allied/tamed Bestiary entries — has an `owner` property that takes a link. That link can point to any PC, any NPC, or **[[Player Characters/The Party/The Party|The Party]]**, a dedicated entity that exists purely to be a selectable owner for group-held things (pooled gear, a jointly-bought wagon, a rented room nobody's individually claimed). The Party is tagged `#party`, not `#pc` — it deliberately doesn't show up in the Party Roster or anywhere else that expects a real character's race/class.

Two places to see ownership: [[Player Characters/The Party/The Party|The Party's]] own page shows everything owned collectively; [[Ownership]] in the Indexes shows everything, grouped by owner, across every ownable type at once. Each PC's Inventory page (or, for Hilda, her main sheet) also has its own live "Owned Items" section scoped to just that character.

By design, this only tracks things worth a full page (magic items, named gear, a bought property) — it's deliberately not a system for logging every ration and coin each player is personally carrying. What one player keeps in their own pockets day-to-day is their business, not something the vault (or the DM) needs to track.

**Creating an ownable thing**: every Item, Companion, and Residence template prompts you for an owner (The Party, or one of the four PCs) the moment you create it via QuickAdd or Templater — pick "— none / set manually —" if it belongs to an NPC instead, then fill `owner` in by hand. A Downtime Activity page has its own "Items Acquired" section pointing back to this same flow, so something crafted or bought during downtime can become a fully-owned Item page in one step. Stackable items (potions, arrows, rations) also carry a `quantity` field instead of needing one page per copy.

## Relationship Graph

The **Relations** plugin renders a visual graph from the `friend` / `rival` / `ally` / `enemy` / `family` (etc.) properties already used on PC and NPC pages — open it from the ribbon icon or Command Palette → "Relations: Open relations view". It's already configured to use `npcimage` for portraits and needs no further setup; it just needs those relationship properties to actually be filled in on pages to have something to draw. Add a relationship field to any PC or NPC page and it appears in the graph next time you open it.

## Cross-Referencing NPCs, Quests, and Locations

The pattern that keeps these in sync without manual duplication: a **Quest** page lists the NPCs, locations, and PCs involved in its own `related-npcs`/`related-locations`/`related-pcs` properties. An **NPC** page doesn't need to separately track which quests it's in — its "Active Quests" section is a Dataview query that scans every quest for a link back to that NPC where `status` is Active. If you add an NPC to a quest, that NPC's own page picks it up automatically the next time it's opened. The same logic drives the Quest Board and Faction Reputation indexes.

## Publishing / Sharing

Before sharing this vault (or parts of it) with friends, check [[Publish Readiness]]. It sorts every NPC, Location, Item, Group, Bestiary, Companion, PC, and Session-Notes page into **Ready to Publish**, **In Progress**, or **Stub** — purely by scanning each page's own text for the vault's placeholder conventions ("Placeholder", "Not yet discovered") relative to how many sections it has. Nothing to maintain by hand: name a page and leave it empty, and it shows up as a Stub automatically; write real content into it, and it graduates on its own the next time the page is read. Use it to decide what's safe to hand someone a link to right now versus what needs a pass first.

## If Something Isn't Populating

Almost always one of these:

1. A property is blank even though the visible table shows something — check the file's Properties panel (or raw frontmatter) directly.
2. A note that should show up somewhere is still tagged `#template` — it was probably created by copy-paste instead of Templater/QuickAdd.
3. A Dataview query needs `DataviewJS` enabled and it isn't (see above).
4. A cross-reference (like an NPC's Active Quests) depends on the _other_ note's property being set — e.g. the quest needs the NPC linked in `related-npcs`, not the other way around.

## Plugins This Vault Depends On

Dataview, Templater, QuickAdd, Meta Bind, Tag Wrangler, Supercharged Links (colors links by `type:` — see its settings if the colors look off), Relations (powers the `friend`/`rival`/`ally` relationship fields on PC and NPC pages), 5e Statblocks and the DM Compendium (for rendering monster/spell reference content). If a page looks broken (raw `INPUT[...]` text, no color-coding, missing Dataview tables), check that the relevant plugin is actually enabled first.
