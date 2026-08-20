# Core Gameplay & Shop Setup

This guide introduces the complete lifecycle of creating and operating a shop in survival mode.

---

## 1. Core Principles

In EurekaBusiness, a shop is not an abstract menu—it is a physical building constructed in the Minecraft world.
- **Server Authoritative**: All transactions, inventory updates, profit calculations, and customer AI decisions execute on the server.
- **Visual Operations**: Customers walk into the shop, browse items on display pedestals, express thoughts via speech bubbles, and queue up at the cash register to check out.

---

## 2. Prerequisites

Building a functional shop requires the following core items and blocks:
1. **Shop Configurator**: Defines the 3D shop boundary and sets customer entrance and exit locations.
2. **Key Device**: The physical on/off operational switch of the shop.
3. **Shop Key**: Stores ownership data and coordinates of the bound Key Device.
4. **Cash Register & Cashier Handle**: The physical settlement counter where revenue is collected.
5. **Display Pedestal & Price Tag Module**: Displays goods and publishes prices to prospective buyers.

---

## 3. Step 1: Define Shop Boundaries

Hold the **Shop Configurator**:
1. **Switch Mode**: Hold the interaction key or open the radial menu, selecting `Bounds` mode.
2. **Select Corners**: Sneak-right-click a block to set corner A, then right-click an opposing diagonal block to define the 3D AABB region.
3. **Set Entrance & Exit**:
   - Switch to `Set Entrance` mode and right-click ground blocks where customers should enter.
   - Switch to `Set Exit` mode and right-click ground blocks where customers should leave.
   - Note: Multiple entrances and exits are supported. Customers choose the shortest accessible route.

---

## 4. Step 2: Bind the Key Device & Open the Shop

1. Place a **Key Device** inside the shop boundary.
2. Use the Shop Configurator to bind the Key Device to the shop region, generating a unique **Shop Key**.
3. **Open the Shop**:
   - Insert the Shop Key into the Key Device. The device lights up, projects the shop boundary, and transitions the shop to the `OPEN` state.
   - Customer NPCs will begin spawning at designated entrances and walking into the shop.
4. **Close the Shop**:
   - Remove the Shop Key. The shop enters a drain gate: existing shoppers finish their purchases and leave, while no new customers spawn.

---

## 5. Step 3: Display Goods & Settle Sales

1. Place **Display Pedestals** and deposit sale items.
2. Attach **Price Tag Modules** and set price bands (see [Display Pedestals, Pricing & Settlement](Shop-Management.md)).
3. Place a **Cash Register** and **Cashier Handle**, then assign a cashier clerk or pull the handle manually.
4. Customers pick up items into their shopping baskets and line up at the cash register. Pulling the handle settles the transaction and stores earnings in the equipped Value Container.
