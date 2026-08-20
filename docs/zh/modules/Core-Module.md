# Core 模块与公共 API

Core 是 EurekaBusiness 的平台基础模块。它面向 Retail、Restaurant 和附属模组提供内容中立的公共契约。

## 主要公共 API

| API | 用途 |
| --- | --- |
| `QualifiedTypeId` | 跨模块使用的稳定限定 ID |
| `ElementDefinition` | 注册要素的不可变定义 |
| `ElementRegistrar` | 启动期注册要素并在结束时冻结注册表 |
| `ElementView` | 冻结后的只读要素视图 |
| `CustomerVariantRegistrar` | 注册顾客呈现变体 |
| `CustomerVariantDefinition` | 顾客变体的不可变定义 |
| `ElementRarityAlgorithm` | 读取店铺要素画像的稀有度算法基类 |
| `CustomerContinuePurchaseAlgorithm` | 购买后决定是否继续购物的函数契约 |
| `ElementContinuePurchaseAlgorithm` | 使用商品要素和店铺画像的连购算法基类 |

## 要素定义

要素由限定 ID、翻译键、图标资源和可选的 `0xRRGGBB` 专属色调组成。要素定义本身不包含价格，也不绑定具体物品；具体商品由所属业务模块在目录中分配要素及 `1..9` 等级。

## 冻结只读视图

注册阶段结束后，Core 将发布不可变视图。运行时读取要素和顾客变体应统一使用只读视图，不应保留可变注册器的引用。

## 依赖与访问规范

附属模组应严格依赖公开 API，禁止引用 `internal` 内部包、平台私有实现或客户端专属类。若所需能力尚未在公共契约中开放，应先在 Core 模块中设计并扩充 API，禁止使用反射访问内部私有字段。
