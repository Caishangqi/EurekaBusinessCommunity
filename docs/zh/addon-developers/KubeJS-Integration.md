# Retail KubeJS 集成

`EurekaBusiness Retail KubeJS` 是 Retail 的可选适配器。它提供受限的声明式脚本接口，用于扩展顾客、装饰、商品目录、小费和部分顾客策略。脚本不能直接操作交易、库存、寻路或顾客行为。

## 安装

专用服务器和连接到启用适配器服务器的客户端都需要安装以下内容：

- EurekaBusiness Core 和 Retail。
- `eureka-business-retail-kubejs-neoforge` 适配器。
- 与适配器兼容的 KubeJS。

`startupContent` 声明若引用方块、模型或其他内容，客户端还必须能生成相同的结构性声明，并提供通过 `resource()` 显式列出的资源。仅供 `serverContent` 使用的服务器覆层不属于这项连接校验。

适配器注册两个 KubeJS 事件：

- `EurekaBusinessEvents.startupContent` 用于结构性内容。
- `EurekaBusinessEvents.serverContent` 用于可重载的服务器覆层。

## 内容层次与重载

Retail 按以下顺序组合内容：

1. 内置默认值。
2. 服务器 Fzzy Config。
3. KubeJS 服务器脚本覆层。

`startupContent` 必须放在 `kubejs/startup_scripts`。它可声明要素、Retail 顾客变体和装饰定义。连接校验比较服务器与客户端生成的结构性声明摘要，以及通过 `resource()` 显式声明的资源。脚本文件不必逐个相同，只要生成的声明与资源结果一致。修改结构性内容后需要重启。

`serverContent` 必须放在 `kubejs/server_scripts`。它会在服务器资源重载时重新计算，可通过 `/reload` 更新。每次重载从当前 Fzzy Config 内容重新开始，删除脚本声明也会移除该覆层中的对应修改。

无效的候选内容不会部分应用。Retail 会保留最后一次接受的快照，并在服务器日志中记录诊断。已经生成的顾客、已评估价格、预留、结算和小费义务会继续使用生成或评估时冻结的事实。重载只影响之后的顾客和新的服务器决策。

## 结构性声明

下面的例子使用普通 KubeJS 方块注册，并把该方块和一个原版方块声明为装饰：

```js
StartupEvents.registry('minecraft:block', event => {
  event.create('shop_charm').displayName('Shop Charm')
})

EurekaBusinessEvents.startupContent(event => {
  event.decoration('kubejs:shop_charm', 'kubejs:shop_charm')
    .flat(15)

  event.decoration('kubejs:stone_display', 'minecraft:stone')
    .element('eurekabusinesscore:element_terra', 5)
})
```

`event.decoration(id, blockId)` 接受任意已注册且默认状态不是空气的原版方块、模组方块或普通 KubeJS 方块。一个方块 ID 只能对应一个装饰定义。声明的装饰会成为店铺内顾客的寻路障碍，顾客不能穿过、站在其上方或把它当作跳板。这个规则只影响 Retail 顾客，不改变方块在世界中的碰撞、交互或其他实体寻路行为。

不要把顾客需要经过的地板、楼梯或通道方块声明为装饰。没有方块物品的已注册方块可以声明，但玩家不能用普通物品放置它。

旧的 `eurekabusinessretailkubejs:shop_decoration` builder 已移除。已放置的旧 builder 方块不会自动替换。升级前请备份世界，在旧版本中替换方块并更新脚本。

## 服务器覆层

`serverContent` 提供的是声明式编辑器。它只收集受验证的数据，不会把实时注册表、实体、库存或服务器对象交给脚本。

```js
EurekaBusinessEvents.serverContent(event => {
  event.catalogPut('minecraft:amethyst_shard',
    5, 15,
    16, 45,
    46, 90,
    91, 150)
  event.catalogAddElement('minecraft:amethyst_shard',
    'eurekabusinesscore:element_vitreus', 2)

  event.enableVariant('eurekabusinessretail:customer.mage')
  event.variantPolicy('eurekabusinessretail:customer.mage')
    .spawnCycle(300, 600)
    .spawnBatch(1, 2)
    .fixedRarity(25)

  event.decorationFlat('kubejs:shop_charm', 20)
})
```

可用的目录操作包括：

- `catalogHas`、`catalogGet`、`catalogList`。
- `catalogPut`、`catalogRemove`。
- `catalogSetElement`、`catalogClearElements`、`catalogAddElement`、`catalogRemoveElement`。

顾客操作包括：

- `enableVariant`、`disableVariant` 和 `variant`。
- `variantPolicy` 中的生成周期、生成批量、购买画像、浏览预算、寻路预算、漫游画像、稀有度和连购规则。
- `tips(variantId)` 中的固定值、百分比、要素百分比和物品奖励规则。

装饰操作包括 `decorationFlat`、`decorationElement`、`enableDecoration` 和 `disableDecoration`。服务器配置不能把已有装饰改指向另一个方块，也不能禁用内置回退顾客变体。目录物品、要素、变体、装饰和小费奖励都必须引用已注册的完整 ID。

## 脚本边界

适配器不提供任意业务脚本执行入口。不要在交易、服务器 tick、寻路或顾客行为中运行任意 JavaScript。使用上述声明式事件表达需要变更的内容，其他游戏逻辑仍由 Retail 服务端维护。

有关内置装饰效果，请阅读[店铺装饰品](../items/Decorations.md)。有关 Fzzy Config 商品目录设置，请阅读[陈列基座与价格牌](../items/Pedestals-and-Price-Tags.md)。
