# 顾客变体与 AI 算法开发 (Customer Variants and AI)

本文档面向 Core/Retail 附属模组作者。

## 顾客变体定义

使用 `CustomerVariantDefinition.builder(variantId, npcType)` 构造不可变定义，再通过 `CustomerVariantRegistrar` 注册。定义需要提供翻译键、至少一组模型和肖像、稀有度算法、生成周期、生成批次、购买画像、浏览预算和导航预算。

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

`model`、`portrait`、预算和生成参数必须使用当前 API 中的实际定义。上例重点展示注册契约，不提供未经项目验证的数值。

## 元素稀有度算法

继承 `ElementRarityAlgorithm`，从上下文读取店铺元素画像：

```java
public final class AlchemistRarity extends ElementRarityAlgorithm {
    @Override
    public int percentage(CustomerRarityContext context) {
        QualifiedTypeId magic = elementId("eurekabusinesscore:element_praecantatio");
        return hasElement(context, magic) ? 10 + levelOf(context, magic) * 5 : 0;
    }
}
```

算法只读取 `CustomerRarityContext`，返回值由公共契约按 `0..100` 处理。店铺画像在服务端生成顾客时构建，不应在算法中逐 tick 扫描店铺。

## 连购算法

实现 `CustomerContinuePurchaseAlgorithm`，或继承 `ElementContinuePurchaseAlgorithm` 读取购买商品元素和店铺画像：

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

`continuePurchase` 可以省略；省略时变体保留原有的受上限约束的购买行为。算法不能修改库存、结算或实体状态。

## Tint 模型变体

`CustomerModelVariant` 可以声明可选的整体 `tint`。多个变体可以共享同一模型、纹理和动画，仅通过不同 tint 提供视觉变化。Tint 只影响客户端呈现，不改变顾客权限、价格或购买结果。

## 运行时边界

顾客的选择、价格、库存、购物篮和结算均由服务端决定。客户端只呈现模型、肖像、Tooltip、Hover Tip、Face Highlight 或其他 UI 状态。
