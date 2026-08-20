# 配置文件与 Schema 迁移指南

本文档面向整合包作者。Retail 的商品目录由服务端配置驱动，客户端不作为目录状态的权威来源。

## 配置文件

Retail 使用 Fzzy Config 注册配置 `eurekabusinessretail:value_catalog`。配置文件位于游戏实例的 `config/` 目录下。

核心字段包括：

| 字段 | 作用 |
| --- | --- |
| `catalogEntries` | 可售物品目录，每项包含物品 ID、元素列表和四档价格区间 |
| `purchaseQuantityMin` | 单笔购买数量下限 |
| `purchaseQuantityMax` | 单笔购买数量上限 |

每个目录项包含 `itemId`、`elements`、`cheap`、`perfect`、`expensive` 和 `overpriced`。价格区间为闭区间；未填写固定价格时，系统使用区间中点作为基准展示价格。

## 元素配置

每个元素配置项结构如下：

```toml
[[catalogEntries]]
itemId = "minecraft:book"

[[catalogEntries.elements]]
elementId = "eurekabusinesscore:element_cognitio"
level = 1
```

`level` 在发布目录时限制在 `1..9` 范围内。元素 ID 必须是 Core 已注册的完整键（例如 `eurekabusinesscore:element_terra`）。包含未知物品或未知元素的条目会导致整个目录更新被拒绝，服务端将保留最近一次有效快照。

## Schema 版本演进

当前目录配置 Schema 版本为 **5**：

- 低于版本 4 的旧目录由于使用过废弃的地区字段，升级时会重置为内置默认目录。
- 版本 4 的空目录在迁移时会恢复一次默认目录，用于修复早期初始化时序问题。
- 版本 5 允许空目录作为整合包作者的主动配置，正常启动不会自动填充默认商品。

迁移前请备份配置文件。开发环境中可使用根项目的 `resetRetailConfig` Gradle 任务重置 Retail 目录配置，在下一次启动时重新生成最新默认配置。

## 验证流程

1. 在独立测试实例中编辑配置；
2. 确认每个 `itemId` 在当前游戏注册表中有效存在；
3. 确认所有元素使用完整的命名空间注册键，等级处于 `1..9` 区间；
4. 启动专用服务器并检查配置加载日志；
5. 将验证无误的配置文件打包至整合包。

配置仅负责商品目录与基准价格。交易库存、权限、结算和持久化状态仍由服务端权威管理。
