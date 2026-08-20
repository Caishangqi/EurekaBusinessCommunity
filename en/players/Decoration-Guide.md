# Shop Decorations & Area Buffs

This guide explains how to place shop decorations and leverage area buffs to boost merchandise selling prices.

---

## 1. Decorations Overview

Placing decorations within the shop boundary provides operational bonuses to covered display pedestals:

| Decoration Name | Block / Item ID | Effective AABB Bounds | Buff Type | Scaling & Mechanism |
| :--- | :--- | :--- | :--- | :--- |
| **Gecho Gargoyle** | `gecho_gargoyle` | $2 \times 1 \times 2$ centered on block | Flat percentage | **+20%** base selling price for all goods in range |
| **Resounding Horn** | `resounding_horn` | $2 \times 1 \times 2$ projecting forward | Element scaling | **+5%** selling price per level of Magic (`praecantatio`) on the item |

---

## 2. Calculation & Stacking Rules

1. **Automatic Proximity Detection**:
   - When customers evaluate an item on a pedestal, the server automatically queries all active decorations overlapping the pedestal's location.
   - No physical wiring or manual linking is required.
2. **Linear Stacking**:
   - Multiple decoration buffs stack linearly on the same pedestal.
   - Example: An enchanted book with **Magic Lv.3** placed on a pedestal covered by both the Gecho Gargoyle and Resounding Horn receives:
     $$\text{Total Price Bonus} = 20\% + (3 \times 5\%) = +35\%$$
     If the base price is 40 value, final checkout revenue is $\lfloor 40 \times 1.35 \rfloor = 54$ value.
3. **Layout Strategies**:
   - Place Gecho Gargoyles near the shop center to radiate standard retail shelves.
   - Point Resounding Horns directly at dedicated high-tier arcane and magical displays to maximize returns.

---

## 3. Display Pedestal Types & Upgrades

The mod provides three cosmetic pedestal variants:

- **Nomad Pedestal (`nomad_pedestal`)**: Warm natural wood texture for nature and adventure themes;
- **Deepslate Pedestal (`deepslate_pedestal`)**: Dark, heavy deepslate base for arcane and dungeon themes;
- **Stone Pedestal (`stone_pedestal`)**: Clean, classic stone stand for general goods.

All pedestals support the **Price Tag Module (`price_tag`)**, which projects public prices directly above the item.
