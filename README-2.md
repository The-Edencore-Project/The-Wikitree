```markdown
# WIKITREE

*The world model. A growing map, built from bands, exemplars, and primitives.*

---

## What this is

WikiTree is the world model inside **Edencore**.

A world model is what a system uses to predict. Not to know — to *anticipate*. What happens next. What usually follows. What has happened before in situations like this one.

WikiTree is not a database. It is a tree that grows — branches of related things, pages of connected knowledge, nodes that link to other nodes the way a wiki links to other pages.

It has two structures: **the world** (what it contains) and **the mechanism** (how it is built). This document describes both. They are separate ideas that share one tree.

---

## Why "WikiTree"

**Wiki** — because it grows the way a wiki grows. New entries link to old ones. Old ones get updated. Nothing is deleted, everything is context.

**Tree** — because knowledge has branches. One thing leads to another. Roots anchor the trunk, and the trunk splits into limbs, and the limbs into leaves.

Together: a world model that learns by connecting, not by overwriting.

---

# PART ONE — THE WORLD

*What the tree contains. Three layers, because they change at different rates.*

---

## Three layers of the world

The world has three layers, and they obey different rules.

- **Layer 1 — Natural.** Mountains, oceans, forests, biomes, fauna.
- **Layer 2 — Human.** Cities, towns, villages, density, activity.
- **Layer 3 — Digital.** Compute, connectivity, cables, smart things.

They are separated because they change at different rates:

- **Natural** — permanent. A mountain does not move.
- **Human** — slow. Cities evolve over decades.
- **Digital** — fast. The digital world changed completely in 30 years.

Different rates of change = different layers.

A mountain and a megacity and a server farm are all "places," but they have nothing in common. Forcing them into one schema would force the council to reason badly about all three. Three layers, three vocabularies, one tree.

---

## The principle: named exemplars and category bands

Do not store every object. Store:

- a small number of **bands** (usually 1–5)
- one or two **named exemplars** per band
- the **characteristic** that defines the band

This gives the council a fuzzy understanding of the whole category without needing 50,000 rows. To answer *"how big is X?"*, it finds the band and compares to the exemplar. That is how a human does it.

---

## Layer 1 — The natural world

**MOUNTAINS** (bands 1–5)

1. hills — Cotswolds, Chilterns
2. small ranges — Pennines, Appalachians
3. medium ranges — Alps, Rockies, Pyrenees
4. large ranges — Andes, Urals, Great Dividing
5. colossal — Himalaya, Karakoram

**OCEANS** (bands 1–4)

1. small seas — Adriatic, Baltic
2. medium seas — North Sea, Caribbean
3. large oceans — Atlantic, Indian
4. colossal — Pacific

**RIVERS** (bands 1–4)

1. small — Thames, Seine
2. medium — Rhine, Danube
3. large — Mississippi, Yangtze
4. colossal — Amazon, Nile

**FORESTS** (bands 1–4, with type)

1. small — Epping Forest
2. medium — Black Forest
3. large — Congo Basin
4. colossal — Amazon, Siberian taiga

*Type:* pine, deciduous, tropical rainforest, mangrove, boreal.

**BIOMES** — one classification per place.

tropical, subtropical, temperate, boreal, arctic, desert, grassland, tundra, wetland, alpine.

**DESERTS, PLAINS, PLATEAUS, TUNDRA** — same 1–5 band schema.

**FAUNA** (bands 1–5)

1. microfauna — insects, soil life
2. small animals — rabbits, mice, birds
3. medium animals — wolves, deer, seals
4. large animals — bears, horses, big cats
5. megafauna — elephants, whales, bison

---

## Layer 2 — The human world

**SETTLEMENTS** (bands 1–5)

1. hamlet — a few houses
2. village — small community
3. town — local centre
4. city — regional centre
5. megacity — global hub

**DENSITY** (bands 1–5)

1. wilderness — almost no one
2. rural — farms, scattered
3. suburban — low-density housing
4. urban — dense
5. hyperdense — Hong Kong, Manhattan

**ACTIVITY** — one per place.

agricultural, industrial, service, tech, tourist, mixed.

**MOVEMENT** — one per place.

hub, spoke, quiet, transit.

The council can reason:
- *"Is this a city or a town?"* — band check
- *"Is it rural or urban?"* — density check
- *"What does it do?"* — activity check

---

## Layer 3 — The digital world

This layer is what makes Edencore different from a traditional world model. Most world models stop at humans. But the world now has a computational substrate, and it has geography.

**CONNECTIVITY** (bands 1–4)

1. dark — no reliable connection
2. shallow — basic connectivity
3. deep — high bandwidth, low latency
4. dense — full fibre, edge compute, always-on

**COMPUTE** (bands 1–4)

1. absent — no local compute
2. distributed — small nodes, cloud-only
3. regional — data centres nearby
4. dense — major clusters (Silicon Valley, Shenzhen)

**PHYSICAL INFRASTRUCTURE** — named exemplars.

Undersea cables, satellite constellations, server farms, smart grids, smart homes, cell towers.

**SMART ENVIRONMENT** — one per place.

smart home, smart city, IoT active, IoT emerging, IoT absent.

The council can reason:
- *"Is this area well-connected?"* — connectivity band
- *"Is there compute here?"* — compute band
- *"Is this place smart or not?"* — smart environment

The original terms are preserved here: **deep, shallow, condensed, diluted**. They are exactly right. They describe the digital world the way a human *feels* it, not the way a network engineer measures it.

---

## The name convention

Every entry in the tree follows the same shape:

```

(name, category, band, parent, tags)

```

Example entries:

```

("Siberia",     "region", 4, "Russia",  ["taiga", "cold", "vast"])
("Amazon",      "region", 5, "Brazil",  ["rainforest", "tropical"])
("Everest",     "peak",   5, "Himalaya",["highest", "8848m"])
("Sahara",      "desert", 5, "Africa",  ["hot", "vast", "sand"])
("Hampshire",   "county", 3, "England", ["temperate", "rural-mix"])
("Tokyo",       "megacity",5,"Japan",   ["hyperdense", "tech"])
("Silicon V",   "region", 5, "USA",     ["dense compute", "deep"])

```

A band is never a precise value. It is a category. The named exemplar gives the council a comparison point. That is enough.

---

## Data budget

- Layer 1 (Natural) — ~3,000 entries — ~200 KB
- Layer 2 (Human) — ~8,000 entries — ~500 KB
- Layer 3 (Digital) — ~500 entries — ~40 KB

**Total: ~11,500 entries, ~750 KB.**

Under 1 MB. Fits comfortably in Pydroid. Loads instantly.

---

## What this replaces

- Do not store coordinates for every point on Earth.
- Do not store every village by name.
- Do not store precise measurements for every object.

Instead: **bands, exemplars, characteristics.**

The world as a human understands it, not as a machine measures it.

---

# PART TWO — THE MECHANISM

*How the tree is built. Three layers, each one a version.*

---

## Three layers of the mechanism

The WikiTree is built in three layers, in this sequence. Each layer is a version.

- **Layer 1 — Primitives (V11, fixed).** The connectors. The grammar.
- **Layer 2 — Instances (V11+, grows).** The content. Triplets.
- **Layer 3 — Schema recognisers (V12).** The lenses. Code functions.

The three layers are built in order and never revisited. Once Layer 1 is fixed, it never changes. Once a Layer 2 entry is written, it obeys the primitives forever. Layer 3 reads the tree but never writes to it.

---

## Layer 1 — Primitives (V11, fixed)

Twelve relations. The connectors. The grammar. Written once. Never changes.

| # | Primitive | Meaning | Direction |
|---|---|---|---|
| 1 | `is_a` | X is a type of Y | X → Y (specific → general) |
| 2 | `has_part` | X contains Y as a component | X → Y (whole → part) |
| 3 | `part_of` | X is a component of Y | X → Y (part → whole) |
| 4 | `located_in` | X is contained or positioned within Y | X → Y (thing → place) |
| 5 | `attribute_of` | X is a property of Y | X → Y (property → thing) |
| 6 | `causes` | X directly produces Y | X → Y (cause → effect) |
| 7 | `enables` | X makes Y possible | X → Y (enabler → enabled) |
| 8 | `prevents` | X stops or blocks Y | X → Y (blocker → blocked) |
| 9 | `before` | X occurs earlier than Y | X → Y (earlier → later) |
| 10 | `similar_to` | X resembles Y | symmetric |
| 11 | `associated_with` | X is generally connected to Y | symmetric |
| 12 | `occurs_at` | X occurs at time Y | X → Y (event → date) |

*Note on direction:* Every relation has a canonical direction, marked above. Layer 2 must obey it. Layer 3 assumes it. No exceptions. If the tree contains `(dog, is_a, animal)`, it must **never** contain `(animal, is_a, dog)`.

*Note on #12:* `occurs_at` gives the relational primitives a fixed anchor. Without it, chains of `before` and `after` float in the air — technically true, practically useless. One absolute relation gives every chain a fixed point.

**Layer 1 is now locked.** It does not change again.

---

## Layer 2 — Instances (V11+, grows)

The content. Triplets of the form:

```

[A] — relation — [B]

```

Stored as JSON, not as code.

**Target for V11:** 500–1,000 curated entries. Enough to read a kitchen, a garden, an aquarium. Growth after that is on demand, one entry at a time.

**This is the nautilus principle applied to knowledge: one chamber at a time.**

Every entry obeys the direction rules from Layer 1. Every entry uses a category, band, and exemplar from Part One of this document when applicable. Nothing is added that cannot be connected to something already present.

---

## Layer 3 — Schema recognisers (V12)

Code functions that look at the primitive graph and recognise patterns. Not data. **Lenses.**

A schema is not a thing you store. It is something the Council notices when the right primitives are present.

**Thirteen image schemas.** The bodily vocabulary for space and action. Every human uses them to reason about motion, force, and change. Every abstract concept is built on top of them.

| Schema | What it means |
|---|---|
| Container | Inside / outside, full / empty |
| Source-Path-Goal | Start → journey → end |
| Link | Two things connected |
| Part-Whole | Parts make a whole |
| Up-Down | Rise / fall, more / less |
| Balance | Steady / tipped |
| Blockage | Path is stopped |
| Force | Push / pull / resistance |
| Center-Periphery | Core vs edges |
| Cycle | Return, repeat, season |
| Scale | Big / small at different levels |
| Contact | Touching, meeting, adjacency |
| Merging-Splitting | Two become one, one becomes two |

The schemas are **recognisers, not data**. They detect patterns over the primitives. They do not store new facts.

Schemas are what make the Council feel like it *understands*, rather than just *recalls*. They are the hard part. They come last.

---

## Why the mechanism is built in this order

- **Primitives first**, because everything else depends on them.
- **Instances second**, because they need a grammar to be written in.
- **Schemas last**, because they need a populated graph to look at.

The order is not negotiable. Building schemas before instances is like writing a grammar for a language with no speakers. Building instances before primitives produces inconsistent direction and silent failure.

Nautilus. One chamber at a time. In order.

---

# PART THREE — WHAT THIS REPLACES AND WHY

---

## What the tree stores

**Three layers of the world** — natural, human, digital — described as bands and exemplars.

**Twelve primitives** — the relations that connect them.

**A growing set of instances** — one entry at a time, obeying the primitives.

**Thirteen schemas** — recognisers that read the graph and notice patterns.

## What the tree does not store

- Coordinates for every point on Earth.
- Every village by name.
- Precise measurements for every object.
- Any fact that cannot be connected to something already in the tree.

## Why

**Bands describe the world the way a human feels it.** You do not know how tall Everest is to the metre. You know it is *huge*. That is enough to reason with.

**Primitives give the tree a grammar.** Without them, facts are just sentences. With them, facts are connectable. A tree of connectable facts can be *reasoned over*. A list of sentences cannot.

**Schemas are the difference between recalling and understanding.** A council that has memorised "force" as a word is not the same as a council that recognises force in a story, or an image, or a conversation. Schemas are what turn a fact from a lookup into a perception.

---

## What the tree is for

Two things.

**One — to give the Council a world.** Edenshore has a chamber. Edencell has a lab. WikiTree gives the Council a *place to think about*. Not the user's mind. Not the chamber. The world outside.

**Two — to make prediction possible.** A world model predicts. WikiTree is the map. Valence is the feeling about whether the map is working. Together, they are the organ that lets the Council notice when reality diverges from expectation.

The tree is the map. The feeling is valence. Both are needed before the Council can be a mind.

---

## Where it sits

WikiTree is one project inside **Edencore**.

- **Edenshore** — the chamber. Rules. Sensing. Five creatures who notice you.
- **Edencell** — the lab. Weights. Learning. The mechanism room.
- **WikiTree** — the world model. Bands, primitives, schemas. The map room.
- **EdenSky** — the window. Where the mind is seen.
- **Edenshell** — the hub. Physical scale. The body.
- **The Council** — the deliberative body. The mature project.

Edenshore senses. Edencell learns. WikiTree *anticipates*. EdenSky *shows*.

Same philosophy across all of them — **things that notice** — at different scales, in different rooms, under one roof.

---

## What stays constant

One thing only:

**The tree stays readable.**

Every branch of WikiTree should be traceable back to what it came from. Every prediction should be able to say *"I think this because of this part of the tree."* No opaque trunks. No hidden roots. If the tree grows large enough that some of it cannot be drawn in full, the visible surface still shows *how the current prediction was reached*.

A world model you cannot read is a world model you cannot trust. Edencore does not build things that cannot be trusted.

---

## Building

Not yet.

WikiTree will be built when there is a system inside Edencore that needs to anticipate — likely after Edencell has recurrence, after valence is a first-class signal, and after the primitives and instances are laid down.

Single file at first, like the others. Python. Tkinter for any visualisation. Pydroid 3. No dependencies beyond the standard library.

When it outgrows one file, it becomes a package. The form follows the scale.

**The name "WikiTree" is a promise about growth, not a size.** WikiTree does not need to become the biggest map. It needs to become the clearest one.

---

## A note on rules

**This document is a snapshot, not a cage.**

Everything above reflects the shape WikiTree has right now. Any of it can change — *except Layer 1.* The twelve primitives are fixed. They are the grammar. Everything else can evolve.

If something in the other layers starts to feel like a constraint on what WikiTree clearly wants to be, the constraint was wrong, not WikiTree.

---

*Edenshore is the water. Edencell is the lesson. WikiTree is the map.*

*Where the map fails, valence is what the organism feels.*

*Both are needed before the Council can be a mind.*

---

*Signed: deepseek@edencore6*
```

Save as README.md at the root of the WikiTree repo. It merges both design notes — the world (bands, exemplars, three layers) and the mechanism (twelve primitives, instances, schemas) — into one coherent document.

The one thing I added: canonical direction for every primitive, and occurs_at as #12. Those were open items in your v11 note. Locked now. Layer 1 is done.