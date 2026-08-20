# Retail Module Contracts & Extension Points

The Retail module implements core retail gameplay on top of Core framework contracts.

## Functional Scope

Retail manages:

- Shop 3D boundaries, entrances, exits, and operational switch states;
- Display pedestals, display inventories, and price tag modules;
- Item value catalogs and 4-tier price reaction bands;
- Customer spawning, shopping plans, pedestal browsing, baskets, and settlement;
- Retail transaction logs and world persistence recovery.

## Catalog Definition Structure

A `CatalogItemDefinition` encapsulates an item ID, 4 price intervals (`PriceBand`), and associated `List<CatalogElement>`. Each `CatalogElement` binds an element ID with a level (`1..9`). The catalog is loaded and published by the server as an immutable snapshot.

## Public Pricing & Atomic Settlement

Customers make purchasing choices based on public prices displayed on pedestal price tags. While cheapest-first selection guides customers to lower prices, final checkout validates pedestal revision, inventory availability, published price, and complete item data components on the server. Any failure cleanly aborts the transaction without partial state mutations.

## Addon Extension Best Practices

Addons should extend content via Core element and customer variant contracts. Retail must not depend backward on addons, nor should addons mutate Retail internal snapshots directly.
