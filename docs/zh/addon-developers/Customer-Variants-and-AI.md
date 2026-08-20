# 顾客变体与 AI 算法开发

本文档面向 Core 与 Retail 附属模组作者。

## 顾客变体定义

使用 `CustomerVariantDefinition.builder(variantId, npcType)` 构造不可变定义，再通过 `CustomerVariantRegistrar` 注册。定义需要提供翻译键、至少一组模型与肖像、稀有度算法、生成周期、生成批次、购买画像、浏览预算与导航预算。

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

`model`、`portrait`、预算和生成参数必须使用 Core API 中的真实对象。

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

算法只读取 `CustomerRarityContext`，返回值限制在 `0..100` 范围。店铺画像在服务端生成顾客时一次性构建，禁止在算法内扫描方块。

## 连购算法

实现 `CustomerContinuePurchaseAlgorithm`，或继承 `ElementContinuePurchaseAlgorithm`：

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

未显式设置 `continuePurchase` 时，变体保留默认的连购意愿。算法不可修改库存或实体状态。

## 颜色 Tint 模型变体

`CustomerModelVariant` 可以声明可选的整体 `tint`。多个变体可以复用同一几何模型、纹理和动画，仅通过不同颜色代码提供视觉区分。Tint 仅作用于客户端渲染。

## 运行时职责划分

顾客的寻路、价格决策、库存挑选、购物篮和结算全部由服务端权威计算。客户端仅负责渲染模型、肖像、反应气泡与收银台界面。