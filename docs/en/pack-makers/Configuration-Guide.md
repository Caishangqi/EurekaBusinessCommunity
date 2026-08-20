# Configuration & Schema Migration Guide

This document is for modpack authors. Retail value catalogs are server-driven; the client never acts as the authoritative catalog source.

## Configuration Files

Retail uses Fzzy Config to manage the `eurekabusinessretail:value_catalog` configuration, stored under the instance's `config/` directory.

Core parameters:

| Field | Purpose |
| --- | --- |
| `catalogEntries` | List of sellable items, each declaring item IDs, elements, and 4 price bands |
| `purchaseQuantityMin` | Minimum batch purchase quantity per transaction |
| `purchaseQuantityMax` | Maximum batch purchase quantity per transaction |

Each catalog entry defines `itemId`, `elements`, `cheap`, `perfect`, `expensive`, and `overpriced`. Price bands represent closed integer intervals $[min, max]$. When an explicit price is omitted, the midpoint represents the nominal display price.

## Element Configuration

Element definitions within an item entry follow this structure:

```toml
[[catalogEntries]]
itemId = "minecraft:book"

[[catalogEntries.elements]]
elementId = "eurekabusinesscore:element_cognitio"
level = 1
```

`level` is clamped to `1..9` upon catalog publishing. The element ID must match an active Core registry key (e.g. `eurekabusinesscore:element_terra`). Entries referencing unregistered items or elements are rejected, preserving the previous valid snapshot.

## Schema Version History

The current configuration Schema version is **5**:

- Versions prior to 4 used obsolete region fields and automatically reset to the built-in defaults upon upgrade.
- Version 4 empty catalogs were restored once during migration to resolve early initialization races.
- Version 5 treats an empty catalog as an intentional configuration, preventing unwanted default overwrites on normal launches.

Always back up configuration files before upgrading modpack versions. In development workspaces, use `./gradlew resetRetailConfig` to regenerate fresh default configurations under `runs/`.

## Verification Guidelines

1. Test catalog modifications in an isolated game profile;
2. Verify all `itemId` entries exist in the active Minecraft registry;
3. Ensure element keys use full namespaced IDs with levels between `1` and `9`;
4. Check dedicated server launch logs for configuration reload events;
5. Distribute verified configuration files within the final modpack release.
