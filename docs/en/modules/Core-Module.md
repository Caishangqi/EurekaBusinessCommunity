# Core Module Public API Contracts

Core forms the architectural foundation of EurekaBusiness, offering domain-neutral contracts for Retail, Restaurant, and downstream addons.

## Primary Public APIs

| API | Purpose |
| --- | --- |
| `QualifiedTypeId` | Immutable namespaced identifier used across modules |
| `ElementDefinition` | Immutable descriptor of a registered element |
| `ElementRegistrar` | Bootstrap registrar for element definitions |
| `ElementView` | Frozen, read-only query view of active elements |
| `CustomerVariantRegistrar` | Bootstrap registrar for customer appearance and AI variants |
| `CustomerVariantDefinition` | Immutable definition of a customer variant |
| `ElementRarityAlgorithm` | Base class for rarity evaluation against shop element profiles |
| `CustomerContinuePurchaseAlgorithm` | Contract deciding continuous purchasing appetite |
| `ElementContinuePurchaseAlgorithm` | Element-driven continuous purchase evaluation base |

## Element Definitions

Elements declare a qualified ID, translation key, 16×16 icon asset, and an optional `0xRRGGBB` tint color. Elements contain no pricing or item associations; domain modules assign elements and levels (`1..9`) to catalog items.

## Frozen Read-Only Views

Following the bootstrap phase, Core freezes all registries into immutable views. Runtime components query these read-only views and discard mutable registrar references.

## Dependency Boundaries

Addons must depend only on exported API contracts. Never import `internal` packages or access private fields via reflection.
