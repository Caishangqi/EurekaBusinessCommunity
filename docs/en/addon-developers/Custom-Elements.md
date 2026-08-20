# Custom Elements & Registration

This document explains how addon authors can declare and register custom elements during the Core initialization window.

## Element Definition

An `ElementDefinition` declares:

- `QualifiedTypeId id`: Namespaced identifier, typically `yourmod:element_<name>`;
- `String translationKey`: Localization key, e.g. `element.yourmod.crystal`;
- `CustomerAssetId iconAsset`: Path to the element's icon asset;
- `int tintColor`: Optional `0xRRGGBB` tint color, or `ElementDefinition.NO_TINT`.

Example declaration:

```java
import com.eureka.eurekabusiness.core.api.business.QualifiedTypeId;
import com.eureka.eurekabusiness.core.api.element.ElementDefinition;
import com.eureka.eurekabusiness.core.api.element.ElementRegistrar;
import com.eureka.eurekabusiness.core.api.npc.customer.CustomerAssetId;

QualifiedTypeId id = QualifiedTypeId.parse("yourmod:element_crystal");
ElementDefinition definition = new ElementDefinition(
        id,
        "element.yourmod.crystal",
        CustomerAssetId.parse("yourmod:textures/gui/elements/crystal.png"),
        0x80FFFF
);

ElementRegistrar registrar = /* obtain during the Core bootstrap window */ null;
```

Registrars are provided through framework lifecycle callbacks. Never invoke registries via reflection or static state after freeze.

## Assets & Localization

Icons are client resources, while element metadata is shared across logical sides. Provide 16×16 texture assets in your mod resources alongside translations in `en_us.json` and `zh_cn.json`.

## Item Element Levels

Element definitions do not hardcode item levels. Retail assigns levels (`1..9`) to registered elements per catalog entry via `CatalogElement`.

## Design Rules

- Element IDs must be globally unique;
- Registration must complete before registry freeze;
- Use qualified type IDs, not localized display names, when referencing elements;
- Do not store prices, inventories, or customer permissions inside element definitions.
