# 坐标轴(Axes)

坐标轴是图表的组成部分。它们用于确定数据如何映射到图表上的像素值。在笛卡尔图表中，有1个或多个X轴和1个或多个Y轴将点映射到2维画布上。这些轴被称为[笛卡尔轴(cartesian axes)](./cartesian/README.md#cartesian-axes)。

在径向图表中，如雷达图或极地面积图，有一个单一轴可以在角度和径向方向上映射点。这些被称为[径向轴(radial axes)](./radial/README.md#radial-axes)。

2.0版本以上的Chart.js的刻度选项比1.0版本更强大，但也有些许不同。

* 支持多 X轴 和 Y轴
* 内置的标签auto-skip特性可以检测到重叠的刻度和标签，然后移除所有第n个标签以保持正常显示。
* 支持缩放标题
* 无需编写全新的图表类型即可扩展新的比例类型

# 通用配置

以下属性对Chart.js提供的所有坐标轴都是通用的

| 名称        | 类型      | 默认值 | 描述                                                                                                             |
| ----------- | --------- | ------ | ---------------------------------------------------------------------------------------------------------------- |
| `display`   | `Boolean` | `true` | 如果设置为`false` ，则该坐标轴从视图中隐藏。覆盖 _gridLines.display_, _scaleLabel.display_, and _ticks.display_. |
| `callbacks` | `Object`  |        | 坐标轴生命周期的回调函数钩子 [更多...](#callbacks)                                                               |
| `weight`    | `Number`  | `0`    | 坐标轴排序权重，数值越高离图标区域越远                                                                           |

## 回调

以下回调函数可用于更改更新过程中不同点处的比例参数

| 名称 | 参数 | 描述 |
| ---- | ---- | ---- |---------------------------------------- |
| `beforeUpdate`                | `axis`    | 在更新之前回调                       |
| `beforeSetDimensions`         | `axis`    | 在设置尺寸之前回调                          |
| `afterSetDimensions`          | `axis`    | 在设置尺寸之后回调                            |
| `beforeDataLimits`            | `axis`    | 在确定数据限制之前回调                   |
| `afterDataLimits`             | `axis`    | 在确定数据限制之后回调                   |
| `beforeBuildTicks`            | `axis`    | 在ticks创建之前回调                           |
| `afterBuildTicks`             | `axis`    | 在ticks创建之后回调。用于过滤ticks |
| `beforeTickToLabelConversion` | `axis`    | 在把ticks转换为字符之前回调        |
| `afterTickToLabelConversion`  | `axis`    | 在把ticks转换为字符之后回调             |
| `beforeCalculateTickRotation` | `axis`    | 在 tick rotation被确定之前回调|
| `afterCalculateTickRotation`  | `axis`    | 在 tick rotation被确定之后回调 |
| `beforeFit`                   | `axis`    | 在比例适合canvas前的回调                 |
| `afterFit`                    | `axis`    | 在比例适合canvas后的回调                  |
| `afterUpdate`                 | `axis`    | 更新结束后回调                    |

## 更新坐标轴默认值

默认配置的刻度可以使用scale service更改。只需传入部分配置片段，和当前默认配置合并，形成新的配置。

例如，要为所有线性比例设置最小值0，您可以执行以下操作。在此之后创建的任何线性比例都具有最小值0。

```javascript
Chart.scaleService.updateScaleDefaults("linear", {
	ticks: {
		min: 0
	}
});
```

## 创建新的坐标轴

要创建新的坐标轴，请参考[开发者文档](../developers/axes.md).
