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

[Wiki: Civics](https://stellaris.paradoxwikis.com/ID#Civics). Also listed in `common\governments\civics` folder.

## Traits

```
add_trait_species <species ID> <trait ID>
```

[Wiki: Species_traits](https://stellaris.paradoxwikis.com/ID#Species_traits). Also listed in `common\traits` folder.

## Leaders

The Beholder
```
event paragon.1
```

Astrocreator Azaryn
```
event paragon.228
```

List good planets for her to terraform

```
effect ordered_planet_within_border = { limit = { planet_size > 25 is_planet_class = pc_barren NOT = { has_modifier = "terraforming_candidate" } } position = 0 order_by = trigger:planet_size inverse = no set_variable = { which = Size_Of_Planet value = trigger:planet_size } custom_tooltip = "[This.GetName] is an Azaryn candidate, in system [This.System.GetName]" }
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
effect random_owned_ship = { ship_event = { id = galactic_features.303 } }
```

Nameless Apostate
```
event crisis.21125
```

Oracle
```
event ancrel.4036
```

Zadigal
```
event astral_planes.3100
```

Mercedes Romero
```
event astral_planes.6105
```

Ceriz t'Xal
```
event grand_archive.1070
```

Ruuk Qabruuk
```
event grand_archive.1080
```

Captain Ness
```
event grand_archive.8570
```

## Relics

Add relics
```
add_relic all
```

Remove a relic
```
effect remove_relic = r_severed_head
```

Remove relic activation countdown
```
effect remove_modifier = relic_activation_cooldown
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
