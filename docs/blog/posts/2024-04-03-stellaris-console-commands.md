---
title: Stellaris console commands
date: 2024-04-02
tags:
  - games
---

+ [Stellaris console commands](https://stellaris.paradoxwikis.com/Console_commands)
+ [Stellaris IDs](https://stellaris.paradoxwikis.com/ID)
+ [Stellaris cheats](https://stellarischeats.com)
+ [Stellaris mods](https://stellaris.smods.ru)

<!-- more -->

## Civics

```
effect force_add_civic = <civic_id>
```

[Wiki](https://stellaris.paradoxwikis.com/ID#Civics). Also listed in `common\governments\civics` folder.

## Traits

```
add_trait_species <species ID> <trait ID>
```

[Wiki](https://stellaris.paradoxwikis.com/ID#Species_traits). Also listed in `common\traits` folder.

## Leaders

The Beholder
```
event paragon.1
```

Astrocreator Azaryn
```
event paragon.228
```

Keides, Scion of Vagros
```
event paragon.3115
```

Curator paragon
```
event leviathans.590
```

Gray
```
event graygoo.406
```

Skrand Sharpbeak
```
event paragon.3001
event paragon.3005
```

S875.1 Warform (need to select a science vessel)
```
effect random_owned_ship = { ship_event = { id = distar.156 } }
```

Caretaker AX7-b	(need to select a science vessel)
```
effect random_owned_ship = { ship_event = { id = distar.245 } }
```

Tuborek (need to select a science vessel)
```
effect random_owned_ship = { ship_event = { id = galactic_features.3035 } }
```

Nameless Apostate
```
event crisis.21125
```

## Relics

Add relics
```
add_relic all
```

Remove a relic, an example
```
effect remove_relic = r_severed_head
```

## Buildings

Contained Ecosphere (resource)
```
event paragon.241
```

Class-4 Singularity	(energy)
```
event ancrel.10009
```

Dimensional Fabricator (minerals)
```
event ancrel.10006
```
