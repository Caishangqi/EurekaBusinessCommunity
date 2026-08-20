# Core 模块与公共 API (Core Module)

Core 是 EurekaBusiness 的平台基础模块。它面向 Retail,Restaurant 和附属模组提供内容中立的公共契约。

## 主要公共 API

| API | 用途 |
| --- | --- |
| `QualifiedTypeId` | 跨模块使用的稳定限定 ID |
| `ElementDefinition` | 一个注册元素的不可变定义 |
| `ElementRegistrar` | 启动期注册元素并冻结注册表 |
| `ElementView` | 冻结后的只读元素视图 |
| `CustomerVariantRegistrar` | 注册顾客呈现变体 |
| `CustomerVariantDefinition` | 顾客变体的不可变定义 |
| `ElementRarityAlgorithm` | 读取店铺元素画像的稀有度算法基类 |
| `CustomerContinuePurchaseAlgorithm` | 购买后决定是否继续购物的契约 |
| `ElementContinuePurchaseAlgorithm` | 使用商品元素和店铺画像的连购算法基类 |

## 元素定义

元素由 ID,翻译键,图标资源和可选 `0xRRGGBB` 色调组成。元素定义不包含价格，也不决定具体商品；商品所属模块负责给目录项分配元素及 `1..9` 等级。

## 冻结视图

注册完成后，Core 发布不可变视图。运行时读取元素和顾客变体应使用只读视图，不应保留可变注册器引用。

## 依赖要求

附属模组应依赖公开 API，不要引用 `internal` 包,平台私有 Registry 实现或客户端实现类。若能力尚未出现在公开契约中，应先提出 Core API 设计，而不是通过反射访问内部状态。
