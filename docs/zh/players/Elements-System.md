# 48 种要素属性与商品 Lore 系统

在 EurekaBusiness 中，每个商品不仅具有价格，还附带其独特的要素属性。要素系统完全取代了旧有的单一地区标签，提供了更加丰富的商品属性体系。

---

## 1. 要素系统概述

- **设计背景**：要素系统灵感来源于经典的神秘时代要素与物质类型体系。
- **等级机制**：每个要素附带等级（范围为 `1 ~ 9`）。更高的要素等级代表该商品在该特性上的纯度或强度。
- **核心作用**：
  1. **顾客生成与偏好**：不同的顾客变体（如炼金术士、探险家）对特定的要素有强烈兴趣。
  2. **刺激连购**：当顾客买到符合其偏好要素的高等级商品时，会激发其在店内继续选购的意愿。
  3. **定价与估值**：整合包作者可以根据商品所含的要素等级设定其默认公允价值。

---

## 2. 物品提示栏呈现

当玩家将鼠标悬停在已识别价值的商品上时，商品 Lore 界面将按如下结构呈现：

```
┌──────────────────────────────────────────────┐
│  铁镐                                         │
├──────────────────────────────────────────────┤
│  [超值价]  [公道价]  [昂贵价]  [天价]         │
│                                              │
│          [ ⛏ 2 ]   [ ⚙ 1 ]   [ ⚒ 1 ]         │
│          (居中排列的要素图标与等级角标)       │
└──────────────────────────────────────────────┘
```

- **第一行**：四档价格反应区间（超值、合理、偏贵、拒买）。
- **第二行**：**居中排列** 的要素图标行。
  - 每个要素以 16×16 剪影图标展示，并带有该要素特有的着色（Tint）。
  - 图标右下角标有金色的等级数字（`1` ~ `9`）。

---

## 3. 48 种官方默认要素列表

Core 模块内置了 48 种要素定义，包含拉丁名、中文译名与专属色调：

| 注册标识符 | 拉丁名 | 中文名 | 专属色调 | 代表概念 |
| :--- | :--- | :--- | :--- | :--- |
| `eurekabusinesscore:element_aer` | `aer` | 风 | `#FFFF7E` | 气体、气流、轻盈 |
| `eurekabusinesscore:element_terra` | `terra` | 地 | `#56C000` | 大地、泥土、稳固 |
| `eurekabusinesscore:element_ignis` | `ignis` | 火 | `#FF5A01` | 火焰、高温、能量 |
| `eurekabusinesscore:element_aqua` | `aqua` | 水 | `#3CD4FC` | 水流、液体、清澈 |
| `eurekabusinesscore:element_ordo` | `ordo` | 秩序 | `#D5D4EC` | 规则、纯净、结构 |
| `eurekabusinesscore:element_perditio` | `perditio` | 混沌 | `#404040` | 熵增、破坏、混乱 |
| `eurekabusinesscore:element_vacuos` | `vacuos` | 虚空 | `#888888` | 虚无、空间、空洞 |
| `eurekabusinesscore:element_lux` | `lux` | 光明 | `#FFF663` | 光照、神圣、视界 |
| `eurekabusinesscore:element_motus` | `motus` | 运动 | `#CDCCF4` | 速度、位移、动量 |
| `eurekabusinesscore:element_gelum` | `gelum` | 寒冰 | `#E1FFFF` | 严寒、冰霜、凝结 |
| `eurekabusinesscore:element_vitreus` | `vitreus` | 水晶 | `#80FFFF` | 透明、晶体、折射 |
| `eurekabusinesscore:element_metallum` | `metallum` | 金属 | `#64647C` | 坚硬、延展、矿石 |
| `eurekabusinesscore:element_mortuus` | `mortuus` | 死亡 | `#887788` | 凋零、终结、腐朽 |
| `eurekabusinesscore:element_victus` | `victus` | 生命 | `#DE0005` | 活力、生机、治愈 |
| `eurekabusinesscore:element_potentia` | `potentia` | 能量 | `#C0FFFF` | 充能、动力、法力 |
| `eurekabusinesscore:element_permutatio` | `permutatio` | 交换 | `#578357` | 转化、置换、等价 |
| `eurekabusinesscore:element_praecantatio` | `praecantatio` | 魔法 | `#9700C0` | 奥术、咒语、附魔 |
| `eurekabusinesscore:element_auram` | `auram` | 灵气 | `#FFC0FF` | 魔力、灵质、源力 |
| `eurekabusinesscore:element_vitium` | `vitium` | 腐化 | `#800080` | 污秽、侵蚀、变异 |
| `eurekabusinesscore:element_tenebrae` | `tenebrae` | 黑暗 | `#222222` | 阴影、幽邃、盲目 |
| `eurekabusinesscore:element_alienis` | `alienis` | 异域 | `#805080` | 末地、维度、未知 |
| `eurekabusinesscore:element_volatus` | `volatus` | 飞行 | `#E7E7D7` | 翱翔、浮空、翅膀 |
| `eurekabusinesscore:element_herba` | `herba` | 植物 | `#01AC00` | 草木、花卉、自然 |
| `eurekabusinesscore:element_instrumentum` | `instrumentum` | 工具 | `#4040EE` | 制造、工具、辅助 |
| `eurekabusinesscore:element_fabrico` | `fabrico` | 合成 | `#809D80` | 组装、锻造、配方 |
| `eurekabusinesscore:element_machina` | `machina` | 机械 | `#8080A0` | 齿轮、工程、自动化 |
| `eurekabusinesscore:element_vinculum` | `vinculum` | 陷阱 | `#9A8080` | 束缚、封印、锁链 |
| `eurekabusinesscore:element_exanimis` | `exanimis` | 亡灵 | `#3A4000` | 骷髅、僵尸、不息 |
| `eurekabusinesscore:element_cognitio` | `cognitio` | 思维 | `#FFC2B3` | 记忆、智力、学习 |
| `eurekabusinesscore:element_sensus` | `sensus` | 感知 | `#C0FFC0` | 五感、洞察、侦测 |
| `eurekabusinesscore:element_bestia` | `bestia` | 野兽 | `#9F6409` | 动物、捕食、野性 |
| `eurekabusinesscore:element_humanus` | `humanus` | 人类 | `#FFD7C0` | 社会、文明、理性 |
| `eurekabusinesscore:element_spiritus` | `spiritus` | 灵魂 | `#EBEBFB` | 幽魂、精神、核心 |
| `eurekabusinesscore:element_lucrum` | `lucrum` | 贪婪 | `#E6BE44` | 财富、金钱、交易 |
| `eurekabusinesscore:element_telum` | `telum` | 武器 | `#C05050` | 剑刃、伤害、战力 |
| `eurekabusinesscore:element_tutamen` | `tutamen` | 装备 | `#00C0C0` | 防具、护盾、坚守 |
| `eurekabusinesscore:element_tempestas` | `tempestas` | 气候 | `#FFFFFF` | 雷暴、风雨、天象 |
| `eurekabusinesscore:element_venenum` | `venenum` | 剧毒 | `#89F000` | 毒素、腐蚀、衰亡 |
| `eurekabusinesscore:element_arbor` | `arbor` | 木头 | `#876531` | 原木、木材、森林 |
| `eurekabusinesscore:element_corpus` | `corpus` | 肉体 | `#EE478D` | 躯体、组织、肌肉 |
| `eurekabusinesscore:element_fames` | `fames` | 饥饿 | `#9A0303` | 进食、渴望、空腹 |
| `eurekabusinesscore:element_iter` | `iter` | 旅行 | `#E0585B` | 远足、路标、探索 |
| `eurekabusinesscore:element_limus` | `limus` | 粘液 | `#01F800` | 史莱姆、弹性、粘滞 |
| `eurekabusinesscore:element_messis` | `messis` | 作物 | `#E1B34E` | 农耕、谷物、收成 |
| `eurekabusinesscore:element_meto` | `meto` | 收获 | `#EE8800` | 采集、劳作、成熟 |
| `eurekabusinesscore:element_pannus` | `pannus` | 布匹 | `#EAEAC2` | 羊毛、皮革、织物 |
| `eurekabusinesscore:element_perfodio` | `perfodio` | 采掘 | `#D5ACAC` | 挖掘、矿工、洞穴 |
| `eurekabusinesscore:element_sano` | `sano` | 治愈 | `#FF92A5` | 恢复、再生、急救 |
