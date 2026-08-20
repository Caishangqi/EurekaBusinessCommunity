# Customer Variants & AI Algorithms

This guide explains how to declare custom customer variants, integrate models, and write AI algorithms.

## Customer Variant Definition

Construct an immutable definition with `CustomerVariantDefinition.builder(variantId, npcType)` and register it via `CustomerVariantRegistrar`:

```java
CustomerVariantDefinition definition = CustomerVariantDefinition.builder(
        QualifiedTypeId.parse("yourmod:alchemist"),
        QualifiedTypeId.parse("eurekabusinessretail:customer")
)
.translationKey("customer_variant.yourmod.alchemist")
.model(modelVariant)
.portrait(portrait)
.interest("eurekabusinesscore:element_praecantatio")
.rarity(new AlchemistRarity())
.spawnCycle(spawnCycle)
.spawnBatch(spawnBatch)
.purchaseProfile(purchaseProfile)
.browseBudget(browseBudget)
.navigationBudget(navigationBudget)
.continuePurchase(new AlchemistContinuePurchase())
.build();
```

Provide valid models, portraits, budgets, and lifecycle parameters from the Core API.

## Element Rarity Algorithms

Extend `ElementRarityAlgorithm` to query the Shop Element Profile:

```java
public final class AlchemistRarity extends ElementRarityAlgorithm {
    @Override
    public int percentage(CustomerRarityContext context) {
        QualifiedTypeId magic = elementId("eurekabusinesscore:element_praecantatio");
        return hasElement(context, magic) ? 10 + levelOf(context, magic) * 5 : 0;
    }
}
```

The algorithm reads `CustomerRarityContext` and returns a clamped probability (`0..100`). The Shop Element Profile is prepared on the server prior to spawning; never scan world blocks from within an algorithm.

## Continue Purchase Algorithms

Implement `CustomerContinuePurchaseAlgorithm` or extend `ElementContinuePurchaseAlgorithm`:

```java
public final class AlchemistContinuePurchase extends ElementContinuePurchaseAlgorithm {
    @Override
    public int continueChancePercentage(CustomerContinuePurchaseContext context) {
        QualifiedTypeId magic = elementId("eurekabusinesscore:element_praecantatio");
        int chance = itemHas(context, magic) ? 10 : 0;
        return CustomerContinuePurchaseAlgorithm.clamp(chance);
    }
}
```

If `continuePurchase` is omitted, the variant uses default purchase caps. Algorithms must remain side-effect-free.

## Tint Color Variants

`CustomerModelVariant` supports an optional color `tint`. Multiple variants can share identical geometry, textures, and animations while displaying distinct clothing colors.

## Server-Authoritative Boundary

Customer pathfinding, price checks, inventory updates, basket state, and settlement calculations execute on the server. The client handles only rendering, portraits, and HUD feedback.
