# 注册自定义要素 (Custom Elements)

本文档面向 Core 附属模组作者。元素注册是启动期行为，运行时注册表冻结后不可修改。

## 元素定义

`ElementDefinition` 包含：

- `QualifiedTypeId id`：推荐使用 `yourmod:element_<name>`。
- `String translationKey`：小写翻译键，例如 `element.yourmod.crystal`。
- `CustomerAssetId iconAsset`：元素图标资源。
- `int tintColor`：可选的 `0xRRGGBB` 着色；无着色使用 `ElementDefinition.NO_TINT`。

示例声明：

```java
import com.eureka.eurekabusiness.core.api.business.QualifiedTypeId;
import com.eureka.eurekabusiness.core.api.element.ElementDefinition;
import com.eureka.eurekabusiness.core.api.element.ElementRegistrar;
import com.eureka.eurekabusiness.core.api.npc.customer.CustomerAssetId;

QualifiedTypeId id = QualifiedTypeId.parse("yourmod:element_crystal");
ElementDefinition definition = new ElementDefinition(
        id,
        "element.yourmod.crystal",
        CustomerAssetId.parse("yourmod:textures/gui/elements/crystal.png"),
        0x80FFFF
);

ElementRegistrar registrar = /* obtain during the Core bootstrap window */ null;
```

上例最后一行只表示类型边界。实际注册器必须由项目提供的生命周期入口传入，不能通过静态猜测或反射获得。

## 资源与翻译

图标是客户端资源，但元素定义本身属于 Core 公共数据。资源应由附属模组随自己的资源包提供，并在 `en_us.json`,`zh_cn.json` 等语言文件中声明翻译键。

## 商品中的等级

元素定义不包含等级。Retail 商品使用 `CatalogElement` 为已注册元素分配 `1..9` 等级；创建 `CatalogElement` 时越界等级会被限制到有效范围。

## 注意事项

- ID 必须全局唯一。
- 注册窗口冻结后不要继续注册。
- 不要使用显示名称代替限定 ID。
- 不要把价格,库存或顾客权限写入元素定义。
