# 注册自定义要素

本文档面向 Core 附属模组作者。要素注册为启动期行为，运行时注册表冻结后不可修改。

## 要素定义结构

`ElementDefinition` 包含以下属性：

- `QualifiedTypeId id`：命名空间限定标识符，推荐格式为 `yourmod:element_<name>`；
- `String translationKey`：语言文件翻译键，例如 `element.yourmod.crystal`；
- `CustomerAssetId iconAsset`：要素图标资源路径；
- `int tintColor`：可选的 `0xRRGGBB` 专属着色；无着色时使用 `ElementDefinition.NO_TINT`。

代码声明示例：

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

实际注册器须由模组提供的生命周期入口传入，不可通过静态单例猜测或反射获取。

## 资源与本地化

图标属于客户端展示资源，但要素定义本身是 Core 跨端公共数据。图标纹理应放置在附属模组的资源包中，并在 `lang/` 语言文件中提供多语言翻译。

## 商品要素等级

要素定义本身不包含具体等级数值。Retail 商品在目录配置中使用 `CatalogElement` 将已注册的要素与 `1..9` 的等级绑定。

## 设计注意事项

- 标识符必须全局唯一；
- 注册表冻结后禁止继续注册；
- 禁止使用显示名称代替限定 ID；
- 要素定义中不得侵入价格、库存或顾客权限逻辑。