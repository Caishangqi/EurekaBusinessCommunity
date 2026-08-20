# Addon API Overview

This document provides development guidelines for NeoForge addon authors extending EurekaBusiness.

## Baseline Constraints

- Target environment: Minecraft `1.21.1` and NeoForge `21.1.x`;
- Depend on `Core` for public contracts, and `Retail` or `Restaurant` for specific domain modules;
- Respect registration lifecycles and physical side boundaries;
- Do not import `internal` packages; never store authoritative server state in client classes.

## Extension Points

### Core Extensions

- Use `ElementRegistrar` to declare domain-neutral elemental aspects;
- Use `CustomerVariantRegistrar` to register customer models, portraits, rarity algorithms, and purchase limits;
- Extend `ElementRarityAlgorithm` to evaluate shop element profiles;
- Implement `CustomerContinuePurchaseAlgorithm` or extend `ElementContinuePurchaseAlgorithm` to define custom shopping persistence.

### Retail Extensions

Retail catalogs, pedestal logic, and trading rules are encapsulated in `Retail`. Addons should interact through public Retail contracts rather than mutating `ValueCatalogSnapshot` or customer entity fields directly.

## Server Authority Principles

All client requests must be validated on the server. Never trust client-supplied item stacks, price amounts, element levels, or target block positions.

## Algorithm Constraints

Rarity and continue-purchase algorithms must be pure, side-effect-free calculations. They read an immutable context and return probability floats or integer limits. Never scan world blocks, mutate inventories, broadcast network packets, or advance entity AI within an algorithm call.

## Verification Requirements

Addon developers should verify:

- Common sources compile cleanly without importing client-only packages;
- Dedicated server boots cleanly without client classes on the classpath;
- Duplicate IDs, unknown elements, and malformed entries fail fast with clear diagnostics;
- Game saves, server restarts, and reconnects correctly preserve custom variant IDs.
