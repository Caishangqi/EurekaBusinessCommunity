# Display Pedestals, Pricing & Settlement

This guide details merchandise management on display pedestals, pricing rules, the cheapest-first selection mechanism, and revenue settlement.

---

## 1. Display Pedestals

The **Display Pedestal** is the primary merchandise selling block in the Retail module:
- **Dynamic Capacity**: Inventory capacity matches the natural maximum stack size of the deposited item (e.g. 16 for ender pearls, 64 for iron ingots), avoiding arbitrary fixed limits.
- **Visual Display**: Items are rendered above the pedestal using a custom Block Entity Renderer (BER) with rotation and hologram projection support.
- **Interaction**:
  - **Right-Click**: Deposit or retrieve held items.
  - **Sneak-Right-Click**: Open the pedestal configuration screen or install augment modules.

---

## 2. Pricing & Price Tag Modules

Pedestals do not publish prices to customers by default. Pricing requires an augment module:
1. **Install Price Tag**: Insert a **Price Tag Module** into an augment slot on the pedestal.
2. **Adjust Price**:
   - The current public price hovers above the tag.
   - Use the **Value Box** interface or right-click the tag to increment or decrement the price.
3. **Customer Psychological Reactions**:
   - When inspecting goods, customers display feedback speech bubbles:
     - **Underpriced**: Highly satisfied; near-certain purchase with boosted continuous buying appetite.
     - **Fair**: Fair market value; purchased according to base willingness.
     - **Overpriced**: Purchased only by high-budget or specialized buyers.
     - **Refusal**: Price exceeds acceptable threshold; customer rejects the item and departs.

---

## 3. Cheapest-First Selection Mechanism

When multiple pedestals offer the exact same item (matching full item ID and data components) at different prices:
- **AI Decision**: Entering customers scan and compare all displayed prices for that item across the shop.
- **Cheapest Priority**: Customers always navigate to the lowest-priced pedestal first.
- **Stock Exhaustion**: Only when the cheapest pedestal is sold out will subsequent customers consider higher-priced alternatives.

---

## 4. Cashier Queuing & Revenue Settlement

1. **Cash Register**:
   - The Cash Register accepts various Value Containers (e.g., currency jars, coin pouches).
2. **Queuing & Portraits**:
   - After picking up goods, customers line up in a single file queue before the Cash Register.
   - The front panel displays the 42×42 portrait of the customer at the head of the line alongside their total checkout amount.
3. **Handle Settlement**:
   - Pulling the **Cashier Handle** triggers an atomic server-side settlement:
     1. Verifies basket items and pedestal reservation integrity;
     2. Deducts items from customer possession and calculates the grand total;
     3. Transfers revenue into the register's equipped Value Container;
     4. Concludes the transaction and releases the customer.
