# 附属模组 API 概览

本文档面向希望为 EurekaBusiness 扩展内容的 NeoForge 模组作者。

## 开发前检查

- 目标环境为 Minecraft `1.21.1` 与 NeoForge `21.1.x`；
- 将 Core 作为公共 API 依赖，将 Retail 或 Restaurant 作为业务模块依赖；
- 遵守公共 API 的生命周期与物理端隔离规则；
- 禁止引用 `internal` 内部包，禁止在客户端类中承载服务端事实。

## 可扩展能力

### Core 模块扩展点

- 使用 `ElementRegistrar` 注册中立的要素定义；
- 使用 `CustomerVariantRegistrar` 注册顾客模型、肖像、稀有度与购买画像；
- 继承 `ElementRarityAlgorithm` 响应店铺要素画像；
- 实现 `CustomerContinuePurchaseAlgorithm` 或继承 `ElementContinuePurchaseAlgorithm` 定制连续购买逻辑。

### Retail 模块扩展点

Retail 的商品目录和交易规则属于 Retail 模块。附属模组应通过公开 Retail 契约接入，避免直接修改 `ValueCatalogSnapshot` 或顾客实体内部私有字段。

## 服务端权威原则

附属模组处理的任何请求均须在服务端重新获取并校验数据。客户端传入的物品、价格、要素等级和目标坐标不可作为交易结算或持久化状态的依据。

## 算法纯函数约束

稀有度与连购算法应当是无副作用的纯计算：根据传入的不可变上下文，返回浮点概率或整数上限。禁止在概率算法中扫描世界方块、修改库存、发送网络数据包或控制实体移动。

## 验证流程

附属模组应至少验证：

- Common 源码编译未引入任何客户端包；
- 专用服务器在无客户端类环境下正常加载公共内容；
- 注册重复 ID、未知要素或非法配置时能抛出明确错误；
- 世界存档、重启和玩家重连后，稳定 ID 与数据正确恢复。
