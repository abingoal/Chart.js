# 笛卡尔轴(Cartesian Axes)

遵循笛卡尔网格的轴被称为“笛卡尔轴”。直角坐标轴用于折线图、条形图和气泡图。 Chart.js 中默认包含四个笛卡尔坐标轴。

* [linear](./linear.md#linear-cartesian-axis)
* [logarithmic](./logarithmic.md#logarithmic-cartesian-axis)
* [category](./category.md#category-cartesian-axis)
* [time](./time.md#time-cartesian-axis)

# 通用配置

所有包含笛卡尔轴的图表都支持多种通用选项。

| 名称         | 类型     | 默认值 | 描述                                                                   |
| ------------ | -------- | ------ | ---------------------------------------------------------------------- |
| `type`       | `String` |        | 图表类型                                                               |
| `position`   | `String` |        | 轴在图表中的位置。可用的值有: `'top'`, `'left'`, `'bottom'`, `'right'` |
| `id`         | `String` |        | 连接数据集和刻度轴的 ID [更多...](#axis-id)                            |
| `gridLines`  | `Object` |        | 网格线配置 [更多...](../styling.md#grid-line-configuration)            |
| `scaleLabel` | `Object` |        | 刻度文字选项 [更多...](../labelling.md#scale-title-configuration)      |
| `ticks`      | `Object` |        | 刻度配置 [更多...](#tick-configuration)                                |

## 坐标轴刻度选项

以下选项对于所有直角坐标轴是通用的，但不适用于其他坐标轴。

| 名称              | 类型      | 默认值  | 描述                                                                                                                 |
| ----------------- | --------- | ------- | -------------------------------------------------------------------------------------------------------------------- |
| `autoSkip`        | `Boolean` | `true`  | 如果为 true，则自动计算可以显示的标签数量并相应地隐藏其他标签。为 false 则任何时候都显示所有的标签。                 |
| `autoSkipPadding` | `Number`  | `0`     | 启用`autoSkip`时，在水平轴上的刻度之间进行填充。 _注意: 仅适用于水平刻度_                                            |
| `labelOffset`     | `Number`  | `0`     | 以像素为单位，用于从标记的中心点（x轴的y方向和y轴的x方向）偏移标签。_注意: 这可能会导致边缘的标签被canvas边缘裁剪掉_ |
| `maxRotation`     | `Number`  | `90`    | 刻度标签的最大旋转角度。 注意: 必要时才会发生旋转 _注意: 仅适用于水平刻度_                                           |
| `minRotation`     | `Number`  | `0`     | 刻度标签的最小旋转。_注意：仅适用于水平刻度_                                                                         |
| `mirror`          | `Boolean` | `false` | 翻转坐标轴上的刻度标签，在图表内显示标签而不是外部。_注意：仅适用于垂直刻度_                                         |
| `padding`         | `Number`  | `10`    | 在刻度标签和坐标轴之间填充。_注意：仅适用于水平刻度_                                                                 |

## 坐标轴ID

属性`dataset.xAxisID`或`dataset.yAxisID`必须与比例属性`scales.xAxes.id`或`scales.yAxes.id`匹配。尤其是在使用多轴图表时，这些属性尤为重要。

```javascript
var myChart = new Chart(ctx, {
	type: "line",
	data: {
		datasets: [
			{
				// 该数据集出现在第一个坐标轴上
				yAxisID: "first-y-axis"
			},
			{
				// 该数据集出现在第二个坐标轴上
				yAxisID: "second-y-axis"
			}
		]
	},
	options: {
		scales: {
			yAxes: [
				{
					id: "first-y-axis",
					type: "linear"
				},
				{
					id: "second-y-axis",
					type: "linear"
				}
			]
		}
	}
});
```

# 创建多坐标轴

使用笛卡尔坐标轴，可以创建多个X轴和Y轴。 为此，您可以将多个配置对象添加到`xAxes`和`yAxes`属性。 在添加新坐标轴时，请确保指定新坐标轴的类型，因为在这种情况下，默认类型是 **not**。

在下面的例子中，我们创建了两个Y轴。然后我们使用`yAxisID`属性将数据集映射到正确的坐标轴。

```javascript
var myChart = new Chart(ctx, {
    type: 'line',
    data: {
        datasets: [{
            data: [20, 50, 100, 75, 25, 0],
            label: 'Left dataset'

            // 将数据集绑定到左侧的y轴
            yAxisID: 'left-y-axis'
        }, {
            data: [0.1, 0.5, 1.0, 2.0, 1.5, 0]
            label: 'Right dataset'

            // 将数据及绑定到右侧的y轴
            yAxisID: 'right-y-axis',
        }],
        labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun']
    },
    options: {
        scales: {
            yAxes: [{
                id: 'left-y-axis',
                type: 'linear',
                position: 'left'
            }, {
                id: 'right-y-axis',
                type: 'linear',
                position: 'right'
            }]
        }
    }
});
```
