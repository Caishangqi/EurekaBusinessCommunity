# Customer Behaviors, Variants & AI

This document introduces customer spawning rules, NPC occupational variants, preference mechanics, and continuous purchasing behavior.

---

## 1. Spawning & Store Entry

1. **Shop Status**: When a valid Shop Key rests inside the Key Device, the shop maintains the `OPEN` state.
2. **Entrances & Spawning**:
   - Customers spawn periodically near configured shop entrances.
   - Powered by a Behavior Tree, customers navigate across the sales floor evaluating accessible pedestals.
3. **Shopping Basket**:
   - Each customer carries a virtual shopping basket holding up to 5 distinct item kinds.

---

## 2. Customer Variants Reference

Customers belong to distinct occupational variants with unique models, textures, portraits, and elemental preferences:

| Variant ID | Name | Model & Portrait | Preferred Elements | Spawning & Rarity Conditions | Shopping & Continue Purchase |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `customer.default` | **Adventurer** | Classic backpack model<br>Portrait: `Gabriel` | General goods | 100% base rarity (fallback) | Base shopping (1-4 items, 50% willingness, 30% threshold) |
| `customer.mage` | **Mage** | Pointed hood & robe models<br>Portraits: `Juan`, `Valdon`, `Violetta` | Magic `praecantatio`<br>Aura `auram`<br>Mind `cognitio` | **Shop Magic Profile**<br>High spawn rate when $\sum \text{Magic} > 4$ | **Arcane Appetite**<br>$+20\% + (\text{Lv} \times 3\%)$ when buying magic items |
| `customer.alchemist` | **Alchemist** | Potion robe model<br>Portraits: `Isaac`, `Jasper`, `Maxine` | Magic `praecantatio`<br>Energy `potentia`<br>Poison `venenum`<br>Taint `vitium` | **Potion & Toxin Profile**<br>Scales with potion and brewing stock | **Alchemy Appetite**<br>$+10\%$ for toxins/potions; boosted by greed items |
| `customer.explorer` | **Explorer** | Trail gear model<br>Portraits: `Amelia`, `Conrad`, `Dylan` | Mining `perfodio`<br>Travel `iter`<br>Metal `metallum`<br>Eldritch `alienis` | **Expedition Profile**<br>Scales with tools, travel gear, compasses, maps | **Expedition Appetite**<br>$+20\% + (\text{Lv} \times 2\%)$ for travel tools |
| `customer.miner` | **Miner** | Mining helmets & pack models<br>Portraits: `Oscar`, `Sasha`, `Evelyn`, `Salvador` | Mining `perfodio`<br>Metal `metallum`<br>Earth `terra` | **Ore & Metal Profile**<br>High spawn rate when $\sum \text{Minerals} > 5$ | **Mining Appetite**<br>$+25\% + (\text{Lv} \times 3\%)$ for raw ores and metals |
| `customer.recolor_0` ~ `recolor_5` | **Traveler (6 Tints)** | 6 custom tinted outfits<br>(Gold, Sky Blue, Emerald, Crimson, Violet, Cyan) | General goods | Fixed 12% rarity | Standard shopping (1-2 items, 50% willingness, 20% threshold) |

---

## 3. Shop Element Profiles & Rarity Sampling

- **Shop Element Profile**:
  - Upon customer spawn ticks, the server computes a snapshot of all active pedestal contents, recording distinct elements, maximum levels, and cumulative element sums ($\sum \text{Element}$).
  - Example: A shop exhibiting an Enchanted Book (`praecantatio` Lv.3), Ghast Tear (`praecantatio` Lv.2), and Blaze Rod (`potentia` Lv.2) yields `praecantatio_sum=5` and `potentia_sum=2`.
- **Dynamic Rarity Sampling**:
  - Variant selection algorithms evaluate the Shop Element Profile:
    - High magic levels and sums attract Mages and Alchemists;
    - High mining, earth, and metal sums draw Miners and Explorers.

---

## 4. Continuous Purchase Mechanism

Customers do not always leave immediately after purchasing an item.

```mermaid
flowchart TD
    Bought[Purchase item from current pedestal] --> Roll[Sample Continue Purchase Algorithm]
    Roll -- Success & Basket not full --> Next[Search next pedestal<br>Continue browsing]
    Roll -- Fail or Target count reached --> Queue[Walk to Cash Register<br>Queue for settlement]
```

- **Algorithm Mechanics**:
  - Following each successful purchase, the variant algorithm computes the continuous purchase chance based on item elements and shop atmosphere.
  - **Satisfaction Bonus**: Underpriced bargains or preferred elements substantially increase the chance to continue shopping.
  - **Basket Caps**: Hard limits ensure customers proceed to the cash register once their purchase target is satisfied.
