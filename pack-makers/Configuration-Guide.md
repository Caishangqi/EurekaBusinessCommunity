# 配置文件与 Schema 迁移指南 (Configuration Guide)

本文档面向整合包作者。Retail 的商品目录由服务端配置驱动，客户端不会成为目录状态的权威来源。

## 配置文件

Retail 使用 Fzzy Config 注册独立配置 `eurekabusinessretail:value_catalog`。配置文件由模组运行环境管理，具体文件位置取决于启动目录，通常位于实例的 `config/` 目录下。

核心字段包括：

| 字段 | 作用 |
| --- | --- |
| `catalogEntries` | 可售物品目录，每项包含物品 ID、元素列表和四档价格区间 |
| `purchaseQuantityMin` | 单笔购买数量下限 |
| `purchaseQuantityMax` | 单笔购买数量上限 |

每个目录项包含 `itemId`、`elements`、`cheap`、`perfect`、`expensive` 和 `overpriced`。价格区间是闭区间；未填写固定价格时，系统使用区间中点作为展示价格。

## 元素配置

每个元素配置项包含：

```toml
[[catalogEntries]]
itemId = "minecraft:book"

[[catalogEntries.elements]]
elementId = "eurekabusinesscore:element_cognitio"
level = 1
```

`level` 会在发布目录时限制到 `1..9`。元素 ID 必须是 Core 已注册的完整键，例如 `eurekabusinesscore:element_terra`。未知物品或未知元素会使这次目录更新被拒绝，并保留最近一次有效快照。

## Schema 版本

当前目录配置 Schema 为 **5**：

- 低于版本 4 的旧目录使用过已移除的地区字段，升级时会重置为代码中的默认目录。
- 版本 4 的空目录只在迁移时恢复一次默认目录，用于修复早期初始化时序问题。
- 版本 5 中空目录可以是作者的有意配置，正常启动不会自动重新填充默认商品。

迁移前请备份配置文件。开发环境可以使用根项目的 `resetRetailConfig` Gradle 任务删除 `runs/` 下的 Retail 目录配置，使其在下一次启动时重新生成默认配置。该任务是开发辅助工具，不是玩家运行时迁移机制。

## 验证建议

1. 先在测试实例中修改目录。
2. 确认每个 `itemId` 是当前注册表中的物品。
3. 确认元素使用完整注册键，等级位于 `1..9`。
4. 启动专用服务器并检查配置更新日志。
5. 再将经过验证的配置复制到整合包发布实例。

配置只负责目录和价格。交易库存、权限、结算和持久化状态仍由服务端运行时校验。
