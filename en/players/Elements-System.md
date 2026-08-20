# 48 Elements & Item Lore System

In EurekaBusiness, items carry unique **Element** attributes alongside prices, establishing a rich classification and economic system.

---

## 1. Elements Overview

- **Design Inspiration**: Inspired by the classic Thaumcraft aspect and elemental philosophy.
- **Level Scaling**: Each element carries a level from `1` to `9`. Higher levels reflect greater purity and intensity of that aspect.
- **Key Functions**:
  1. **Customer Spawning & Preferences**: Diverse customer variants (such as Alchemists, Mages, Miners, Explorers) show strong affinity for specific elements.
  2. **Continuous Purchases**: Buying high-level items matching their preferred elements boosts continuous purchase probability.
  3. **Valuation & Pricing**: Pack authors can configure default fair prices based on elemental compositions.

---

## 2. Item Tooltip & Lore Layout

When hovering over an item with recognized value, the lore box displays:

```
┌──────────────────────────────────────────────┐
│  Iron Pickaxe                                │
├──────────────────────────────────────────────┤
│  [Underpriced] [Fair] [Overpriced] [Refusal] │
│                                              │
│          [ ⛏ 2 ]   [ ⚙ 1 ]   [ ⚒ 1 ]         │
│          (Centered element icons + level)    │
└──────────────────────────────────────────────┘
```

- **Top Row**: Four-tier price reaction bands (Underpriced, Fair, Overpriced, Refusal).
- **Bottom Row**: **Centered** row of element icons.
  - Each element displays as a 16×16 silhouette icon with its characteristic color tint.
  - Golden numeric badges in the lower-right corner indicate the element level (`1` to `9`).

---

## 3. 48 Registered Default Elements

The Core module registers 48 authoritative elements:

| Qualified Identifier | Latin Aspect | Common Name | Tint Hex | Concepts |
| :--- | :--- | :--- | :--- | :--- |
| `eurekabusinesscore:element_aer` | `aer` | Air | `#FFFF7E` | Gas, breeze, lightness |
| `eurekabusinesscore:element_terra` | `terra` | Earth | `#56C000` | Earth, soil, solidity |
| `eurekabusinesscore:element_ignis` | `ignis` | Fire | `#FF5A01` | Fire, heat, energy |
| `eurekabusinesscore:element_aqua` | `aqua` | Water | `#3CD4FC` | Water, flow, fluid |
| `eurekabusinesscore:element_ordo` | `ordo` | Order | `#D5D4EC` | Order, purity, structure |
| `eurekabusinesscore:element_perditio` | `perditio` | Entropy | `#404040` | Entropy, destruction, decay |
| `eurekabusinesscore:element_vacuos` | `vacuos` | Void | `#888888` | Void, space, emptiness |
| `eurekabusinesscore:element_lux` | `lux` | Light | `#FFF663` | Light, brilliance, vision |
| `eurekabusinesscore:element_motus` | `motus` | Motion | `#CDCCF4` | Speed, movement, momentum |
| `eurekabusinesscore:element_gelum` | `gelum` | Frost | `#E1FFFF` | Cold, ice, frost |
| `eurekabusinesscore:element_vitreus` | `vitreus` | Crystal | `#80FFFF` | Crystal, glass, refraction |
| `eurekabusinesscore:element_metallum` | `metallum` | Metal | `#64647C` | Metal, hardness, ore |
| `eurekabusinesscore:element_mortuus` | `mortuus` | Death | `#887788` | Death, decay, ending |
| `eurekabusinesscore:element_victus` | `victus` | Life | `#DE0005` | Life, vitality, healing |
| `eurekabusinesscore:element_potentia` | `potentia` | Energy | `#C0FFFF` | Energy, power, potency |
| `eurekabusinesscore:element_permutatio` | `permutatio` | Exchange | `#578357` | Exchange, barter, trade |
| `eurekabusinesscore:element_praecantatio` | `praecantatio` | Magic | `#9700C0` | Magic, arcane, sorcery |
| `eurekabusinesscore:element_auram` | `auram` | Aura | `#FFC0FF` | Aura, mana, quintessence |
| `eurekabusinesscore:element_vitium` | `vitium` | Taint | `#800080` | Taint, corruption, blight |
| `eurekabusinesscore:element_tenebrae` | `tenebrae` | Darkness | `#222222` | Darkness, shadow, blind |
| `eurekabusinesscore:element_alienis` | `alienis` | Eldritch | `#805080` | End, otherworldly, alien |
| `eurekabusinesscore:element_volatus` | `volatus` | Flight | `#E7E7D7` | Flight, wings, levitation |
| `eurekabusinesscore:element_herba` | `herba` | Plant | `#01AC00` | Flora, grass, nature |
| `eurekabusinesscore:element_instrumentum` | `instrumentum` | Tool | `#4040EE` | Tools, crafting, utility |
| `eurekabusinesscore:element_fabrico` | `fabrico` | Craft | `#809D80` | Manufacturing, forging |
| `eurekabusinesscore:element_machina` | `machina` | Machine | `#8080A0` | Mechanisms, engineering |
| `eurekabusinesscore:element_vinculum` | `vinculum` | Trap | `#9A8080` | Binding, chains, prison |
| `eurekabusinesscore:element_exanimis` | `exanimis` | Undead | `#3A4000` | Undead, skeleton, zombie |
| `eurekabusinesscore:element_cognitio` | `cognitio` | Mind | `#FFC2B3` | Mind, intelligence, logic |
| `eurekabusinesscore:element_sensus` | `sensus` | Senses | `#C0FFC0` | Senses, sight, perception |
| `eurekabusinesscore:element_bestia` | `bestia` | Beast | `#9F6409` | Beast, predator, animal |
| `eurekabusinesscore:element_humanus` | `humanus` | Human | `#FFD7C0` | Humanity, society, reason |
| `eurekabusinesscore:element_spiritus` | `spiritus` | Soul | `#EBEBFB` | Soul, spirit, ghost |
| `eurekabusinesscore:element_lucrum` | `lucrum` | Greed | `#E6BE44` | Wealth, coin, commerce |
| `eurekabusinesscore:element_telum` | `telum` | Weapon | `#C05050` | Weapon, sword, combat |
| `eurekabusinesscore:element_tutamen` | `tutamen` | Armor | `#00C0C0` | Armor, protection, shield |
| `eurekabusinesscore:element_tempestas` | `tempestas` | Weather | `#FFFFFF` | Storm, lightning, tempest |
| `eurekabusinesscore:element_venenum` | `venenum` | Poison | `#89F000` | Poison, toxin, venom |
| `eurekabusinesscore:element_arbor` | `arbor` | Wood | `#876531` | Wood, timber, forest |
| `eurekabusinesscore:element_corpus` | `corpus` | Flesh | `#EE478D` | Body, flesh, muscle |
| `eurekabusinesscore:element_fames` | `fames` | Hunger | `#9A0303` | Hunger, starvation, feast |
| `eurekabusinesscore:element_iter` | `iter` | Travel | `#E0585B` | Travel, journey, walking |
| `eurekabusinesscore:element_limus` | `limus` | Slime | `#01F800` | Slime, elasticity, viscous |
| `eurekabusinesscore:element_messis` | `messis` | Crop | `#E1B34E` | Harvest, crops, grain |
| `eurekabusinesscore:element_meto` | `meto` | Reaping | `#EE8800` | Reaping, gathering, labor |
| `eurekabusinesscore:element_pannus` | `pannus` | Cloth | `#EAEAC2` | Wool, leather, cloth |
| `eurekabusinesscore:element_perfodio` | `perfodio` | Mining | `#D5ACAC` | Digging, pickaxe, caves |
| `eurekabusinesscore:element_sano` | `sano` | Healing | `#FF92A5` | Healing, health, remedy |
