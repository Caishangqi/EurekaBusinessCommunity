# 附属模组 API 概览 (Addon API Overview)

本文档面向希望为 EurekaBusiness 增加内容的 NeoForge 模组作者。

## 开发前检查

- 目标环境为 Minecraft `1.21.1` 和 NeoForge `21.1.x`。
- 将 Core 作为公共 API 依赖，将 Retail 或 Restaurant 作为功能模块依赖。
- 确认公共 API 的生命周期和侧隔离要求。
- 不引用 `internal` 包，不在客户端类中承载服务端事实。

## 可扩展方向

### Core 扩展

- 使用 `ElementRegistrar` 注册内容中立的元素。
- 使用 `CustomerVariantRegistrar` 注册顾客模型、肖像、稀有度和购买画像。
- 继承 `ElementRarityAlgorithm` 读取店铺元素画像。
- 实现 `CustomerContinuePurchaseAlgorithm` 或继承 `ElementContinuePurchaseAlgorithm` 定义连购行为。

### Retail 扩展

Retail 的商品目录和交易规则属于 Retail。附属模组应通过公开 Retail 契约或独立适配层接入，不要直接修改 `ValueCatalogSnapshot`、发现存储或顾客实体内部字段。

## 服务端权威要求

附属模组发送的任何请求都必须在服务端重新获取和校验数据。客户端传入的物品、价格、元素等级和目标坐标不能直接用于交易或持久化。

## 算法约束

算法应是无副作用的业务计算：读取传入的不可变上下文，返回概率或上限。不要在概率算法中扫描世界、修改库存、发送网络包或推进实体行为。

## 验证要求

附属模组至少应分别验证：

- Common 编译不会加载客户端类。
- 专用服务器能够启动并加载缺失客户端环境下的公共内容。
- 注册重复 ID、未知元素和非法配置会得到明确失败结果。
- 保存、重启和重连不会丢失附属内容使用的稳定 ID。
