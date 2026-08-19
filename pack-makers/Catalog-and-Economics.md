# 商品目录与要素经济 (Catalog and Economics)

本文档面向整合包作者，说明如何使用商品目录控制零售内容与经济节奏。

## 默认目录

当前代码种子包含以下示例商品：

| 物品 | 默认元素 |
| --- | --- |
| `minecraft:andesite` | `element_terra:1` |
| `minecraft:netherrack` | `element_ignis:1`, `element_mortuus:1` |
| `minecraft:iron_pickaxe` | `element_instrumentum:2`, `element_metallum:2` |
| `minecraft:iron_axe` | `element_instrumentum:2`, `element_metallum:2` |
| `minecraft:nether_wart` | `element_venenum:1`, `element_praecantatio:1` |
| `minecraft:blaze_powder` | `element_ignis:2`, `element_praecantatio:1` |
| `minecraft:book` | `element_cognitio:1`, `element_praecantatio:1` |

完整键使用 `eurekabusinesscore:element_<latin>` 格式。默认目录是配置的初始种子，不是每次启动都会覆盖作者配置的动态列表。

## 四档价格

每个目录项有四档价格区间：

- `cheap`：低于常规预期的价格。
- `perfect`：理想价格区间。
- `expensive`：偏高但仍可能成交的价格。
- `overpriced`：高价区间。

每个区间可以设置 `start`、`end` 和可选 `stamp`。`stamp` 为负数时使用闭区间中点作为展示价格。价格必须为非负整数，数量和价格的最终合法性由服务端目录快照再次校验。

## 同款商品的竞争

同一个完整物品数据在多个陈列基座出现时，顾客会按公开标价优先选择最低价基座。价格相同时保留供给顺序或原有随机回退行为。整合包作者可以利用这一规则制作促销区，但应同时考虑低价基座的库存与补货能力。

物品比较不能只依赖显示名称。不同数据组件、附魔或自定义数据可能代表不同商品，应使用完整物品数据进行测试。

## 元素与平衡

元素等级是商品属性，不是货币单位。它可以用于：

- 为附属模组的顾客变体提供出现概率条件。
- 为连购算法提供购买后的概率增量。
- 为整合包作者建立主题商品分类和经济梯度。

不要把元素等级直接当作通用价格公式，除非整合包自己的设计明确这样规定。EurekaBusiness 当前只提供元素数据、目录价格区间和顾客扩展契约，不替整合包决定货币模型。
