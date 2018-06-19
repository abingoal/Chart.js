# 类别笛卡尔坐标轴

已经使用过v1.0的童鞋将会很熟悉这个类别刻度。标签是从包含在图表数据中的标签数组中抽取的。如果只定义了`data.labels`，则直接使用。如果定义了`data.xLabels`并且该轴是水平轴，则将使用该数据。同样，如果定义了`data.yLabels`并且该轴是垂直轴，则将使用此属性。同时使用`xLabels`和`yLabels`可以创建一个使用 X 和 Y 轴的字符串的图表。

## 刻度配置选项

类别刻度提供了以下用于配置刻度的选项。它们嵌套在`ticks`子对象中。这些选项扩展了[常用的刻度配置](README.md#tick-configuration)。

| 名称  | 类型     | 默认值 | 米搜书                                             |
| ----- | -------- | ------ | -------------------------------------------------- |
| `min` | `String` |        | 要显示的最小项目 [更多...](#min-max-configuration) |
| `max` | `String` |        | 要显示的最大项目[更多...](#min-max-configuration)  |

## Min Max 配置
对于`min`和`max`属性，该值必须位于`labels`数组中。在下面的例子中，x轴将只显示“March”到“June”的数据。

```javascript
let chart = new Chart(ctx, {
    type: 'line',
    data: {
        datasets: [{
            data: [10, 20, 30, 40, 50, 60]
        }],
        labels: ['January', 'February', 'March', 'April', 'May', 'June'],
    },
    options: {
        scales: {
            xAxes: [{
                ticks: {
                    min: 'March'
                }
            }]
        }
    }
});
```
