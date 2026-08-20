# Item Value Catalog & Element Economics

This document explains how modpack authors can use the value catalog to balance retail pacing and merchandise economics.

---

## 1. Default Catalog & Elements Reference Table

Retail provides 35 balanced default item configuration seeds (managed via Fzzy Config):

| Item ID | Default Elements & Level | Cheap Band [Stamp] | Perfect Band [Stamp] | Expensive Band [Stamp] | Overpriced Band [Refusal] |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **Basic & Construction** | | | | | |
| `minecraft:andesite` | `terra:1` | `1 ~ 10` [8] | `11 ~ 40` [25] | `41 ~ 80` [60] | `81 ~ 120` [100] |
| `minecraft:netherrack` | `ignis:1`, `mortuus:1` | `1 ~ 10` [8] | `11 ~ 40` [25] | `41 ~ 80` [60] | `81 ~ 120` [100] |
| `minecraft:obsidian` | `terra:3`, `tenebrae:2`, `tutamen:2` | `10 ~ 25` [18] | `26 ~ 70` [48] | `71 ~ 140` [105] | `141 ~ 220` [180] |
| **Magic & Arcane** | | | | | |
| `minecraft:book` | `cognitio:1`, `praecantatio:1` | `4 ~ 12` [8] | `13 ~ 40` [26] | `41 ~ 80` [60] | `81 ~ 130` [105] |
| `minecraft:enchanted_book` | `praecantatio:3`, `cognitio:3`, `ordo:2` | `25 ~ 60` [45] | `61 ~ 150` [105] | `151 ~ 300` [225] | `301 ~ 500` [400] |
| `minecraft:ender_pearl` | `alienis:3`, `iter:2` | `15 ~ 35` [25] | `36 ~ 90` [63] | `91 ~ 180` [135] | `181 ~ 280` [230] |
| `minecraft:blaze_rod` | `ignis:3`, `potentia:2`, `praecantatio:1` | `20 ~ 45` [32] | `46 ~ 120` [83] | `121 ~ 220` [170] | `221 ~ 350` [285] |
| `minecraft:ghast_tear` | `spiritus:3`, `sano:2`, `praecantatio:2` | `30 ~ 70` [50] | `71 ~ 180` [125] | `181 ~ 320` [250] | `321 ~ 500` [410] |
| `minecraft:amethyst_shard` | `vitreus:2`, `auram:2`, `praecantatio:1` | `5 ~ 15` [10] | `16 ~ 45` [30] | `46 ~ 90` [68] | `91 ~ 150` [120] |
| **Alchemy & Brewing** | | | | | |
| `minecraft:blaze_powder` | `ignis:2`, `praecantatio:1` | `12 ~ 25` [18] | `26 ~ 70` [48] | `71 ~ 130` [100] | `131 ~ 200` [165] |
| `minecraft:nether_wart` | `venenum:1`, `praecantatio:1` | `5 ~ 12` [8] | `13 ~ 45` [29] | `46 ~ 90` [68] | `91 ~ 140` [115] |
| `minecraft:fermented_spider_eye`| `venenum:2`, `vitium:2`, `praecantatio:1` | `10 ~ 25` [18] | `26 ~ 70` [48] | `71 ~ 130` [100] | `131 ~ 200` [165] |
| `minecraft:magma_cream` | `ignis:2`, `limus:2`, `potentia:1` | `8 ~ 20` [14] | `21 ~ 55` [38] | `56 ~ 110` [83] | `111 ~ 170` [140] |
| `minecraft:spider_eye` | `venenum:1`, `corpus:1` | `3 ~ 8` [5] | `9 ~ 25` [17] | `26 ~ 50` [38] | `51 ~ 80` [65] |
| `minecraft:glass_bottle` | `vitreus:1`, `vacuos:1` | `1 ~ 5` [3] | `6 ~ 18` [12] | `19 ~ 35` [27] | `36 ~ 60` [48] |
| `minecraft:dragon_breath` | `praecantatio:4`, `alienis:3`, `venenum:2` | `40 ~ 90` [65] | `91 ~ 240` [165] | `241 ~ 450` [345] | `451 ~ 700` [575] |
| `minecraft:phantom_membrane` | `volatus:2`, `alienis:1`, `spiritus:1` | `12 ~ 30` [20] | `31 ~ 80` [55] | `81 ~ 150` [115] | `151 ~ 240` [195] |
| **Mining & Metallurgy** | | | | | |
| `minecraft:raw_iron` | `metallum:1`, `terra:1` | `3 ~ 8` [5] | `9 ~ 24` [16] | `25 ~ 50` [37] | `51 ~ 80` [65] |
| `minecraft:raw_gold` | `metallum:2`, `lucrum:2` | `6 ~ 15` [10] | `16 ~ 45` [30] | `46 ~ 90` [68] | `91 ~ 140` [115] |
| `minecraft:raw_copper` | `metallum:1`, `permutatio:1` | `2 ~ 6` [4] | `7 ~ 18` [12] | `19 ~ 38` [28] | `39 ~ 65` [52] |
| `minecraft:coal` | `ignis:1`, `potentia:1`, `terra:1` | `2 ~ 5` [3] | `6 ~ 16` [11] | `17 ~ 32` [24] | `33 ~ 55` [44] |
| `minecraft:iron_ingot` | `metallum:2`, `fabrico:1` | `5 ~ 12` [8] | `13 ~ 35` [24] | `36 ~ 70` [53] | `71 ~ 110` [90] |
| `minecraft:gold_ingot` | `metallum:2`, `lucrum:3` | `10 ~ 22` [16] | `23 ~ 60` [41] | `61 ~ 120` [90] | `121 ~ 190` [155] |
| `minecraft:diamond` | `vitreus:3`, `lucrum:3`, `perfodio:2` | `35 ~ 80` [55] | `81 ~ 220` [150] | `221 ~ 400` [310] | `401 ~ 650` [525] |
| `minecraft:emerald` | `permutatio:3`, `lucrum:3`, `humanus:2` | `25 ~ 60` [40] | `61 ~ 160` [110] | `161 ~ 300` [230] | `301 ~ 480` [390] |
| `minecraft:lapis_lazuli` | `praecantatio:1`, `cognitio:1`, `aqua:1` | `3 ~ 8` [5] | `9 ~ 25` [17] | `26 ~ 52` [39] | `53 ~ 85` [69] |
| `minecraft:redstone` | `machina:2`, `potentia:2`, `motus:1` | `4 ~ 10` [7] | `11 ~ 30` [20] | `31 ~ 60` [45] | `61 ~ 100` [80] |
| **Exploration & Survival** | | | | | |
| `minecraft:iron_pickaxe` | `instrumentum:2`, `metallum:2` | `10 ~ 20` [15] | `21 ~ 60` [40] | `61 ~ 120` [90] | `121 ~ 180` [150] |
| `minecraft:iron_axe` | `instrumentum:2`, `metallum:2` | `8 ~ 18` [13] | `19 ~ 50` [34] | `51 ~ 100` [75] | `101 ~ 160` [130] |
| `minecraft:compass` | `machina:1`, `iter:2`, `cognitio:1` | `8 ~ 20` [14] | `21 ~ 55` [38] | `56 ~ 105` [80] | `106 ~ 165` [135] |
| `minecraft:clock` | `machina:1`, `ordo:2`, `lux:1` | `12 ~ 28` [20] | `29 ~ 75` [52] | `76 ~ 140` [108] | `141 ~ 210` [175] |
| `minecraft:spyglass` | `sensus:3`, `vitreus:2`, `metallum:1` | `15 ~ 35` [24] | `36 ~ 90` [63] | `91 ~ 170` [130] | `171 ~ 260` [215] |
| `minecraft:saddle` | `pannus:2`, `iter:3`, `bestia:2` | `20 ~ 50` [35] | `51 ~ 130` [90] | `131 ~ 240` [185] | `241 ~ 380` [310] |
| `minecraft:golden_apple` | `sano:3`, `victus:3`, `lucrum:2` | `30 ~ 70` [50] | `71 ~ 180` [125] | `181 ~ 340` [260] | `341 ~ 520` [430] |
| `minecraft:echo_shard` | `sensus:3`, `tenebrae:3`, `alienis:2` | `35 ~ 80` [55] | `81 ~ 200` [140] | `201 ~ 380` [290] | `381 ~ 600` [490] |

---

## 2. Value Container Progression

Cash registers utilize Value Containers (`value_container`) featuring a 5-tier upgrade ladder:

| Tier | Capacity | Upgrade Recipe Condition | Emitted Light Level |
| :---: | :---: | :--- | :---: |
| **Tier 0** | `1,024` value | Default recipe | 0 ~ 1 |
| **Tier 1** | `4,096` value | Upgrade full Tier 0 in crafting table | 1 ~ 2 |
| **Tier 2** | `16,384` value | Upgrade full Tier 1 in crafting table | 2 ~ 4 |
| **Tier 3** | `65,536` value | Upgrade full Tier 2 in crafting table | 4 ~ 5 |
| **Tier 4** | `262,144` value | Upgrade full Tier 3 in crafting table | 5 ~ 7 |
| **Tier 5** | `1,048,576` value | Upgrade full Tier 4 in crafting table | 8 (Max) |

---

## 3. Four-Tier Pricing Model

Each entry declares four price bands:

- `cheap`: Substantially below market expectations. Triggers rapid purchases and boosts continuous purchase chances.
- `perfect`: Ideal fair market value. Standard trading balance.
- `expensive`: Elevated price. Accepted only by high-budget buyers.
- `overpriced`: Excessive price. Customers reject the item and leave the shop.

---

## 4. Competition & Item Data Matching

When multiple pedestals display the exact same item, customer AI prioritizes the lowest-priced pedestal. Item matching evaluates the complete item ID and data components (including enchantments, custom names, and NBT data).
